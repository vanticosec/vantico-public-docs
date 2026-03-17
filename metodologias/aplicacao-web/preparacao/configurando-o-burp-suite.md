# Configurando o Burp Suite

Nesta página você vai aprender como configurar e os primeiros passos para utilizar a ferramenta Burp Suite, hoje muito utilizada para pentests em aplicações web.



## Instalação

Para instalar a ferramenta, basta ir na documentação oficial do PortSwigger e fazer o download, segue o link de referência [aqui](https://portswigger.net/burp/documentation/desktop/getting-started/download-and-install).



## Preparando o proxy

O Burp nativamente vem com o Chromium como navegador padrão para sua utilização, para acessar basta ir na aba **Proxy** > **Intercept** > **Open Browser**.

Caso você queira usar um navegador customizado, basta fazer a instalação da extensão **FoxyProxy** e realizar as seguintes configurações.

Na extensão, basta adicionar um nome, hostname e porta, os valores recomendados são **127.0.0.1:8080**, pois são padrões do Burp Suite.

<figure><img src="../../../.gitbook/assets/image (9) (1).png" alt=""><figcaption></figcaption></figure>

No Burp Suite, basta ir em **Settings** > **Proxy** e inserir a interface e porta a mesma inserida na extensão.

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



## Capturando tráfego

Assim que configurado, podemos abrir a aplicação do nosso alvo. Assim que aberto, podemos observar que o tráfego capturado não é apenas do nosso alvo, também é passado diversas requisições para outros hosts e serviços, o que gera uma certa "sujeira" no nosso proxy, para melhorar isso, podemos ir no host que desejamos atacar e adicioná-lo ao escopo, dessa maneira somente seu tráfego irá aparecer na aba "HTTP History".

Para fazer isso, vamos acessar a URL do nosso alvo, em seguida vamos a aba **Targets**. Localize o seu alvo e selecione com o botão direito **Add to scope.**

<figure><img src="../../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Quando selecionado irá aparecer um pop-up, escolha uma das seguintes opções tendo em vista de que:

* Ao escolher **Yes**, você tem certeza de que escolheu todos os possíveis alvos, pois os demais ativos não vão ser interceptados.
* Ao escolher **No**, significa que você ainda não tem certeza se escolheu todos, o que te ajuda a ter um overview melhor sobre a aplicação, caso haja chamadas de API, redirecionamentos externos, etc.

Para mais informações, veja [Scope](https://portswigger.net/burp/documentation/desktop/tools/target/scope).

Uma vez configurado, você agora pode filtrar por apenas o que está no seu escopo, indo na aba **HTTP History** > **Filter Settings** > **Show only in-scope items**.

Aba HTTP History sem aplicar o filtro:

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Aba HTTP History após aplicar o filtro:

<figure><img src="../../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>



Mesmo com o alvo no escopo, as requisições para outros host na aba **Intercept**, permanecem aparecendo, para filtrar isso também, assim que um host indesejado aparecer basta clicar com o botão direito, **Don't intercept requests** > **To this host**.

<figure><img src="../../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>



## Extensões

O Burp Suite permite que você adicione extensões a sua ferramenta, o que possibilita um aumento de capacidades que podem ser realizadas e facilita no processo de entender e encontrar vulnerabilidades, abaixo serão citadas algumas extensões que podem facilitar muito no seu dia a dia, porém antes vamos visualizar como as extensões podem ser obtidas.

Para o funcionamento adequado de algumas extensões, deve ser realizado o download de ambientes como **Java**, **Jython** e **Ruby**, podemos visualizar a seguir o passo a passo para instalação do ambiente **Jython**.

Acessando o site oficial do Jython (pode ser encontrado [aqui](https://www.jython.org/download.html)) você deve selecionar a opção **Jython Standalone JAR**, assim que realizado o download basta inserir na aba de configurações do Burp.

<figure><img src="../../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

Para inserir no Burp basta ir em **Settings** > **Extensions** > **Default settings** e dentro de **Python enviroment** inserir a localização do download do arquivo.

<figure><img src="../../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>



Inserido o ambiente, basta ir em **Extensions** > **BApp Store** e buscar a extensão desejada e em seguida **Install**.

Para mais informações sobre instalação consulte [aqui](https://portswigger.net/burp/documentation/desktop/extend-burp/extensions/installing/bapp-store).

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>



A seguir, algumas das extensões que vão facilitar o seu dia a dia:

1. [Autorize ](https://portswigger.net/bappstore/f9bbac8c4acf4aefa4d7dc92a991af2f)permite identificar falhas de quebra de controle de acesso, como requisições que devem ser realizadas com um token / cookie de autorização, porém podem ser feitas de forma não autenticada.
2. [JWT Editor](https://portswigger.net/bappstore/26aaa5ded2f74beea19e2ed8345a93dd) essa extensão permite em qualquer aba de requisição a visualização e manipulação de tokens JWT, o que facilita a exploração de alguma falha envolvendo o token JWT.
3. [Active Scan++](https://portswigger.net/bappstore/3123d5b5f25c4128894d97ea1acc4976) aumenta as capacidades de scan passivo e ativo do Burp Suite, adicionando verificações que o Burp por padrão não realiza.
4. [Software Vulnerability Scanner](https://portswigger.net/bappstore/c9fb79369b56407792a7104e3c4352fb) essa integração automaticamente detecta por softwares com vulnerabilidades na aplicação web que está sendo acessada.
5. [403 Bypasser](https://portswigger.net/bappstore/444407b96d9c4de0adb7aed89e826122) auxilia no bypass de códigos HTTP 403, alterando os métodos e cabeçalhos da requisição, tenta fazer o downgrade do HTTP (1.1 > 1.0), entre outras formas.
6. [JS Miner](https://portswigger.net/bappstore/0ab7a94d8e11449daaf0fb387431225b) essa extensão vai fazer uma busca em arquivos JS na aplicação, buscando por itens como credenciais, subdomínios, URLs de Cloud, endpoints da API, entre outros, facilitando na fase de recon inicial.



## Recursos

O Burp Suite possui diversos recursos instalados que muitas vezes não são vistos ou lembrados, que podem ajudar bastante durante a realização de um pentest.

A seguir, vamos explicar mais sobre alguns recursos muito interessantes que podem fazer diferença durante seu teste de intrusão.



1. **Unhide hidden inputs**

Este recurso serve para revelar campos escondidos de formulários, o que pode ser muito útil para encontrar falhas como XSS, SQL Injection, SSRF, entre outros.

Para ativar basta ir em **Settings** --> **Tools** --> **Proxy**, descer até o recurso **Response modification rules** e marcar as duas primeiras opções.

<figure><img src="../../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>



2. **Macros**

Essa ferramenta serve para automatizar o processo de inserção do token anti-CSRF que geralmente são gerados novos a cada request, tornando possível inserir um novo token antes de cada nova requisição do **Repeater** ou **Intruder**.

Para acionar, basta ir em **Settings** --> **Sessions** --> **Macros**, depois basta apertar em "**Add**" e ele irá mostrar requests realizados, basta selecionar o que deseja e depois pressionar "**OK**".

<figure><img src="../../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>



3. **Find scripts** (disponível apenas no Professional)

Este mecanismo possibilita buscar todos os arquivos JavaScripts referenciados em uma aplicação web de maneira organizada e instantânea.

Para isso, deve acessar uma aplicação, depois ir na aba **Target** --> clicar com o botão direito --> **Engagement tools** --> **Find scripts**.

<figure><img src="../../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

