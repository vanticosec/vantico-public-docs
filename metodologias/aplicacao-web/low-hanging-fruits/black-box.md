# Black Box

#### **Ausência de cabeçalho**

Toda vulnerabilidade que envolve a **ausência de cabeçalhos ("header")** deve ser adicionada **separadamente** para cada cabeçalho ausente presente no escopo.

Cabeçalhos que devem conter na aplicação web são

* Content-Security-Policy
* X-Content-Type-Options
* Strict-Transport-Security
* Referrer-Policy
* Permissions-Policy

***

#### **Uso de cabeçalho depreciado**

Verificar se a aplicação apresenta cabeçalhos depreciados, como X-Frame-Options, X-XSS-Protection ou Feature-Policy.

Essa validação pode ser feita em conjunto com a identificação da ausência de cabeçalhos.

***

#### Divulgação de informações no cabeçalho HTTP

Outra vulnerabilidade sobre cabeçalhos, esta no caso é quando a aplicação divulga informações como tecnologias, server, no cabeçalho HTTP. Em alguns casos é encontrado como:

_Server: Apache/2.4.52 (Ubuntu)_

***

#### Acesso direto via IP

Ao identificar o endereço IP da aplicação, realize uma requisição com o endereço IP, caso a aplicação não faça o redirecionamento para o endereço DNS a mesma se encontra vulnerável a alguns ataques como bypass de WAF.

***

#### **Ausência do arquivo robots.txt**

Buscar na aplicação o endpoint robots.txt, caso retornado 404 e não demonstrado o campo, a aplicação encontra-se com a falta deste mecanismo.

***

#### **Ausência de WAF**

Identificar se a aplicação possui algum mecanismo de WAF presente.

***

#### **Subdomínios apontando para IPs privados**

Devemos testar se subdomínios da aplicação apontam para endereços privados, para testar isto basta realizar um dig no subdomínio. Caso vulnerável a aplicação pode estar vulnerável a _DNS Rebinding_.

***

#### **CORS Miconfiguration**

Fazer verificações no CORS para validar se o mesmo está muito permissivo e se encontra vulnerável a ataques.

***

#### **Páginas padrão do WordPress**

Algumas páginas do WordPress são padrão e caso não removidas / restringidas, podem auxiliar o processo de reconhecimento, em alguns casos demonstrando a versão utilizada.

Algumas dessas páginas são:

_/readme.txt_

_/license.txt_

_/wp-admin/upgrade.php_

_/wp-admin/install.php_

***

#### **Enumeração de usuários via endpoint WordPress**

O WordPress possui diretórios padrões que permitem a enumeração de usuários válidos da aplicação, sendo eles:

_/wp-json/wp/v2/users_

_/wp-json/wp/v2/users/1_

_/wp-json/oembed/1.0/embed?url=https://{URL.com}_

***

#### **Listagem de diretórios**

Para validar essa vulnerabilidade, basta abrir alguma imagem e voltar um diretório. Também é possível caso enumerado alguns diretórios tentar fazer o acesso direto.

***

#### **Medidas de anti-adulteração de bibliotecas Javascript não estão em uso (Integrity)**

Descrição da integridade do **Sub-recurso** Medidas de detecção de adulteração, como _Subresource Integrity (SRI)_, podem identificar quando um arquivo JavaScript externo importado por um aplicativo foi adulterado por **terceiros mal-intencionados.**

Se não forem obtidos de forma segura, esses arquivos podem ser modificados por invasores para obter **controle** sobre a funcionalidade do arquivo e, portanto, **executar código malicioso** no navegador do usuário usando os privilégios de um site válido.

Vários hackers de roubo de informações de alto nível (em particular contra a British Airways) exploraram esse problema de forma muito eficaz para comprometer **informações confidenciais dos clientes.**

**Então**, procure referências a javascript que não tenha a flag.

**Segue o código abaixo:**

```
integrity="sha384-oqVuAfXRKap7fdgcCY5uykM6+R9GqQ8K/uxy9rx7HNQlGYl1kPzQho
1wx4JwY8wC"
```

***

#### **SSL/TLS**

São protocolos de segurança que garantem que a navegação do usuário fique protegida contra um possível vazamento de dados e ataques hackers. Ou seja, toda a informação sensível compartilhada pelo usuário, se mantém criptografada.

Ambos o SSL quanto o TLS, são muito parecidos, porém o TLS é uma versão mais atualizada do SSL.

**TLS:**

**Transport Layer Security**, este protocolo vai codificando toda a mensagem que o usuário envia ao servidor, e são criados chaves de acesso a qual apenas o emissor e receptor tem acesso e quando a informação faz esse caminho, o TLS autentica quem tentou acessar o conteúdo, caso não seja um dos dois, não é possível acessar a mensagem.

O protocolo TLS é mais eficaz que o protocolo SSL.

Através disto iremos procurar aplicações que contenham cifras fracas, com isso podemos usar o site a seguir:

```
ssllabs.com/ssltest/
```

***

#### **Redirecionamento HTTP**

Esta vulnerabilidade ocorre quando realizado uma requisição para a aplicação com **HTTP** ao invés de **HTTPS**, a maneira recomendada é a aplicação fazer o redirecionamento, caso não fizer, a aplicação encontra-se vulnerável.

***

#### **Vulnerabilidades da versão do server**

Ocorre quando a aplicação divulga informações que podem ajudar um atacante, como a **versão do server** que é utilizada, em que através desta informação, através dessa informação, deve ser realizado uma busca pelo [endoflife](https://endoflife.date/) do serviço e se o mesmo possui vulnerabilidades conhecidas (CVEs).

***

#### **Utilizar bibliotecas JavaScript desatualizadas**

Para encontrar esta vulnerabilidade entramos no código fonte da aplicação, procuramos por arquivos JavaScript, como o **"JQuery"** e sua versão, através desta sua versão um atacante pode buscar por suas vulnerabilidades e explorar uma vulnerabilidade.

***

#### **Gerenciamento de patch insuficiente**

Identificado a versão do produto, buscar CVEs relacionadas e o EndOfLife do produto ([https://endoflife.date/](https://endoflife.date/)).

***

#### **Plugins do WordPress desatualizados**

Alguns plugins do WordPress quando desatualizados podem comprometer a aplicação devido a vulnerabilidades conhecidas, para isto, pode ser feito a validação manualmente ou com ferramentas como o [wpscan](https://github.com/wpscanteam/wpscan) para identificar plugins desatualizados.

***

#### **Js.map**

É uma ótima forma de investigarmos mais sobre a estrutura do site, através de seu código JavaScript.

Primeiro devemos entrar no código fonte da aplicação pressionando CTRL + U, dentro dela iremos procurar por arquivos Javascript.

Iremos buscar sempre o final "js.map" de arquivos como "main" e "app".

Dentro deles iremos procurar no final se contém "js.map".

Então vamos usar uma ferramenta chamada "[decompile\_sourcemap](https://github.com/vanticohq/decompile_sourcemap/tree/main)", através dela usamos o seguinte código como exemplo:

```
python3 decompile_sourcemap.py 
https://example.com/assets/UserNameComplete-d6c0c7fc8bc309d9b022.js.map 
(nome_da_pasta)
```

Em que "(nome\_da\_pasta)" é a pasta que a ferramenta irá criar com o arquivo js.map.

***

#### **Mensagem de Erros**

Quando a aplicação retorna um **erro inesperado** assim que um evento acontece, conforme o retorno que a aplicação der em relação ao erro, o atacante pode entender melhor como funciona a estrutura da aplicação, podendo aproveitar-se de alguma vulnerabilidade que pode ser exposta com o erro.

***

#### **Exposição de chaves API**

Há casos em que dentro de arquivos JavaScript podem ser encontrados credenciais, chaves API e outras informações interessantes, deve sempre verificar estes arquivos.

***

#### **Enumeração de usuários**

Ocorre geralmente na área de login, cadastro ou esqueci a senha, em que quando digitamos algum usuário e senha, a aplicação nos retorna que o usuário já existe, ou que o email não está cadastrado, fazendo com que o atacante consiga enumerar quais usuários/emails são válidos ou não.

Porém o mesmo pode ser encontrado em outras partes da aplicação, como por exemplo alguma aba de alterar o e-mail do usuário dentro da plataforma, pode haver de constar que o e-mail já está cadastrado.

A mensagem correta que a aplicação deve retornar é de **"Usuário ou Senha Incorretos"** ou **"Caso o email já estiver cadastrado você receberá um link na sua caixa de email"** .

A enumeração também pode ser identificada via _time-based_, ou seja, por tempo de resposta, ocorre quando o tempo de resposta quando inserido um usuário válido e inválido são muito diferentes.

***

#### **Ausência de mecanismo contra força bruta**

Essa vulnerabilidade deve ser testada em diferentes campos, como login, redefinição de senha e MFA.

Login: Deve ser testado se há algum controle anti automação ao inserir o mesmo e-mail porém com diversas senhas em um curto período de tempo.

Redefinição de senha: Verificar se possui algum mecanismo ao inserir diversos e-mails no campo.

MFA: Validar se pode ser realizado ataques de força bruta no campo de código do MFA a fim de descobrir a combinação certa para realizar o bypass do mecanismo.

***

#### **Negação de serviço através de múltiplas tentativas de login**

Algumas aplicações impõem (ou não) bloqueio na conta depois de um número de tentativas de acesso, porém muitas vezes esse número pode ser muito grande, permitindo que o atacante tente múltiplas tentativas antes de ser bloqueado, o que também permite um possível ataque de negação de serviço em conjunto.

***

#### **Host header injection**

É quando clicado em "Esqueci a senha", depois ao apertar para enviar a requisição, interceptamos ela e trocar o header "Host" por outro site, caso não redirecionar para lá, mantemos o header Host original e adicionamos abaixo dele o header "X-Forwarded-Host" com o outro site.

Para aumentar a severidade, caso a aplicação seja vulnerável, podemos redirecionar para algum server que temos controle para capturar o token do usuário, possibilitando assim que alteramos a senha do mesmo e ganhamos controle sobre a conta.

***

#### Fuzzing em S3

Ao encontrar um bucket, é necessário realizar um teste de fuzzing a fim de encontar arquivos e diretórios ocultos.

