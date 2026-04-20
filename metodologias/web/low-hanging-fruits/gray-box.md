# Gray Box

#### **Cookie de sessão sem a flag Secure habilitada**

Verificar se o cookie de sessão possui a flag Secure.

***

#### **Cookie de sessão sem a flag HttpOnly habilitada**

Verificar se o cookie de sessão possui a flag HttpOnly.

***

#### Cookie de sessão sem a flag Samesite habilitada

Verificar se o cookie de sessão possui a flag Samesite.

***

#### **Verificações no JWT**

Verificar o que há dentro do token JWT, deve ser reportado caso o token apresente: Criptografia fraca ou dados pessoais e informações sensíveis.

***

#### **Força bruta na assinatura do token JWT**

Caso a aplicação possua tokens JWT, o mesmo deve ser copiado e enviado para tentar quebrá-lo, a fim de obter o valor do _secret_ e assim poder forjar tokens.

Para quebrar podemos utilizar o _hashcat_, seguindo o formato a seguir.

```
hashcat -a 0 -m 16500 token.txt wordlist.txt
```

***

#### **Upload irrestrito de arquivos**

Algumas aplicações possuem funcionalidades de subir arquivos, seja para alterar a foto de perfil, enviar algum documento ou qualquer outra função, porém se a mesma não for sanitizada corretamente é possível fazer o upload de algum arquivo malicioso para realizar diversas ações não autorizadas dentro da aplicação, como abrir uma shell com um arquivo **.php,** executar um arquivo **.exe**, exploit _client-side based_ com um **.html**, etc.

***

#### **Upload de arquivos sem limite de tamanho**

Em alguma funcionalidade de upload de arquivos, deve ser enviado um arquivo com um tamanho maior do que o comum (1GB por exemplo), a fim de verificar se o mesmo vai ser realizado ou não o upload. O envio de um arquivo deste tamanho em algumas aplicações pode causar uma indisponibilidade temporária.

***

#### **Flood em páginas com brute force**

Esta vulnerabilidade se refere a realizar flood em partes específicas da aplicação, como por exemplo: A aplicação possui um campo de criar postagens, neste caso, deve ser realizado um teste de fazer um flood de postagens.

***

#### **Tamanho do cookie maior que 4096 bytes**

Cookies com valores maior de que 4096 bytes podem ocasionar negação de serviço no servidor.

***

#### **Aplicação mostrando hash de senha**

Identificar se a aplicação em alguma rota demonstra o hash de senha do usuário, caso ocorrer, identificar o tipo de hash e se o mesmo possui algum tipo de _salt_.

Para identificar se possui ou não o _salt_, basta codificar a senha inserida no mesmo formato do hash, caso os dois hashes se apresentarem diferente um do outro significa que a aplicação utiliza alguma forma de _salt_ para proteger os hashes de senha.

***

#### **Exposição de metadados em imagens**

Durante o upload de imagens, o sistema deve garantir a remoção dos metadados EXIF antes do armazenamento ou exibição do arquivo. Esses metadados podem conter informações sensíveis, como coordenadas GPS, modelo e marca do dispositivo, data e hora da captura, dados de software e outros detalhes capazes de comprometer a privacidade do usuário.

***

#### **Uso de IDs sequenciais**

Praticamente qualquer sistema moderno tem referências direta a objetos. Este comportamento faz com algumas aplicações utilizem IDs sequenciais, ou seja, se há um objeto de ID 5, o próximo será 6 e assim por diante.

A partir disto pode-se tornar uma vulnerabilidade maior como por exemplo um IDOR.

***

#### **Falta de validação na alteração de dados**

Quando requisitado alguma alteração dentro da área logada, como: **alterar a senha, e-mail ou algum dado pessoal**, a aplicação deve realizar alguma **validação**, que pode ser: requisitar a senha novamente, algum _challenge_ para resolver, e-mail de confirmação, etc.

Caso não haja nenhuma validação é considerado como uma vulnerabilidade.

***

#### **Validação de input insuficiente**

Esta vulnerabilidade ocorre quando a aplicação não valida corretamente a entrada de dados fornecidos pelos usuários, por exemplo, ao criar uma conta, não é validado o e-mail informado, número de telefone ou outro dado solicitado.

Permitindo assim de que haja a criação de contas com dados fictícios ou inválidos e sem a validação adequada, as políticas implementadas, como de senhas fortes, formatos de e-mail, entre outros se tornam ineficazes.

***

#### **Página web armazenando credenciais sem criptografia**

Podemos validar essa vulnerabilidade ao entrar em algum arquivo de javascript presente, dessa maneira devemos buscar alguma credencial exposta em texto claro.

***

#### **Ausência de notifcação por login suspeito**

O sistema não envia nenhum alerta ao titular da conta quando ocorre um login considerado suspeito, por exemplo, de um endereço IP ou localização geográfica nunca antes observados, dispositivo/user‑agent diferente, horário incomum ou após diversas tentativas falhas.

***

#### **Falta de e-mail de verificação no processo de registro**

Validar se durante o processo de registro, é enviado algum e-mail de verificação ao e-mail cadastrado.

***

#### **Falta de aviso para redirecionamento externo**

Qualquer redirecionamento externo que a aplicação realizar com o usuário, deve haver uma notificação precedida a ação.

***

#### **Verificação se o usuário pode alterar a senha**

Deve ser validado se o usuário pode alterar sua própria senha.

***

#### **Token de sessão passado via GET**

Verificar se em alguma requisição o token de sessão é enviado via GET, ou seja, junto com a URL.

***

#### **Aplicação sem mecanismo de logout**

A aplicação deve possuir um mecanismo claro que possibilite o usuário encerrar sua sessão.

***

#### **Ausência de código anti-phishing**

Validar se é possível inserir um código anti-phishing gerado pelo usuário, para assim, quando realizado alguma ação que seja enviado um e-mail ou SMS, seja enviado em conjunto o código criado pelo usuário.

***

#### **Política de senhas permissivas**

Trata-se de quando a aplicação **permite** que o usuário utilize senhas simples e fracas para cadastrar-se, fazendo com que a segurança da aplicação seja mais baixa.

Uma boa política de senhas é aquela em que requer no mínimo 10 caracteres, caracteres especiais, letras maiúsculas e minúsculas e números. Tornando a senha mais complexa e mais difícil do atacante quebrar.

***

#### **Sessão antiga não é invalidada após logout**

Para testar essa vulnerabilidade, enquanto logado na aplicação, deve ser capturado requisição e em seguida realizado o logout, após isto, a requisição capturada anteriormente deve ser repetida a fim de identificar se a mesma ainda funciona ou se o token já foi invalidado.

***

#### **Invalidação do link de redefinição de senha**

Quando clicado em "Esqueci a senha", o link enviado deve ser inválidado após o uso, ou seja, depois de ter trocado a senha, o mesmo link não deve funcionar mais para alterar a senha novamente, a aplicação deve gerar um novo link caso o usuário queira redefinir novamente a senha.

***

#### **DoS JWT**

Em um campo onde inserimos o e-mail e a partir dele é criado um token JWT (de acordo com o e-mail), inserimos um e-mail com diversos caracteres a fim de causar lentidão no momento de geração do token, levando a um possível DoS através do JWT.

***

#### **Invalidação da sessão após troca de senha**

Verificar se ao trocar a senha do usuário a sessão é invalidada. Para testar basta: Capturar uma requisição autenticada, em seguida fazer a troca de senha da conta utilizada, depois repetir a requisição capturada.

***

#### **Ausência de segundo fator de autenticação no procedimento de login**

Quando realizado o login na aplicação a mesma deve haver a opção do usuário ativar o segundo fator de autenticação (MFA).

***

#### **Roubo de conta via redefinição de senha**

Em um campo de redefinição de senha, podemos testar algumas combinações com o intuito de o link de redefinição de senha ou código ser enviado para ambos os usuários (usuário válido e atacante). Algumas das formas são.

Requisição original:

```
{"email":"vitima@pentest.com"}
```

Requisição modificada:

```
{"email":["vitima@pentest.com","pentester@pentest.com"]}
```

Dessa forma, caso vulnerável o e-mail de redefinição será enviado para a vítima e para o atacante.

***

#### **Flood de e-mail por meio de redefinição de senha**

Para realizar o teste dessa vulnerabilidade, devemos: entrar na aba esqueci minha senha, depois inserir o e-mail e interceptar o request quando apertado o botão de enviar, assim com este request, jogamos no repeater e ficamos enviando a mesma requisição diversas vezes, caso todas foram aceitas, irá gerar um flood de e-mails na caixa de entrada do usuário.

***

#### Registro e monitoramento insuficientes

Quando uma aplicação possuir _logs_, deve-se verificar caso a mesma esteja realmente capturando todas as informações que ocorrem na aplicação, pois pode ocorrer de a mesma estar apenas registrando algumas atividades ou refletindo apenas **informações parciais**, o que é uma implicação de **segurança e auditoria**.
