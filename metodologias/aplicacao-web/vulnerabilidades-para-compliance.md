# Vulnerabilidades para compliance

#### Críticas

* Injeção de comandos SQL
* Execução de código remota (RCE)
* Account Takeover
* XSS Armazenado (com payloads relevantes)
* Manipulação de contas sem autorização (realizar ações críticas, alterar senha, exlcusão, alterar e-mail, alterar nome de conta)
* Envio de arquivos maliciosos
* Escalação de privilégios para admin
* CVEs (sendo críticas e funcionais)
* Ataques de força bruta com sucesso
* Serviço acessível na internet (FTP, SSH, Telnet, SMTP, DNS, LDAP, SMB, SFTP, MSSQL, Oracle DB, MySQL, RDP, PostgreSQL, VNC, MongoDB)<br>

#### Altas

* Falta do cabeçalho HTTP Strict Transport Security (HSTS)
* XSS Refletido (e outros)
* Componentes obsoletos (com CVEs)
* TLS depreciado (1.0 e 1.1)
* Injeção de HTML
* Token de sessão não expira após logout
* Política de senhas fracas
* Credenciais em texto claro (exposição ou transmissão)
* Evasão do Cisco Umbrella (teste interno)
* Acesso sem HTTPS (não faz redirecionamento para HTTPS)
* SWEET32, BEAST E LOGJAM (e outras)
* Ataques de força bruta
* Enumeração de usuários
* CVEs (sendo altas)



#### Médias

* Ausência de cabeçalhos (com exceção do HSTS)
* Divulgação de informações no cabeçalho HTTP (Apache, IIS, Nginx)
* CORS
* Componentes obsoletos (sem CVEs)
* Ausência de validação de dados inseridos (por exemplo: <>, &&, (), %00 etc)
* Configuração de TLS incorreta (não faz parte do domínio, usando wildcard (\*), etc)
* Redirecionamento HTTPS para HTTP
* IDOR (com dados não sensíveis)
* CVEs (sendo médias)
* Possibilidade de inclusão de páginas em frames de outro domínio (ambiente externo)
* Suíte de cifras fracas (média/baixa)<br>

#### Baixas

* CVEs (sendo baixas)
* Divulgação de informações no cabeçalho HTTP (jQuery, Next.js, etc)
* Possibilidade de inclusão de páginas em frames de outro domínio (ambiente interno)
* Cookie de sessão sem a flag HttpOnly habilitada
* Divulgação de erros da aplicação (sem informação sensível)
* Credenciais enviadas via método GET<br>

#### Informativas

* Ausência de WAF
* AutoComplete habilitado (sendo possível ver email/usuário salvo via input)
* URL revela alguns dados (?=user ou ?=008, mas não permite realizar IDOR ou outros ataques)
* eTag visível
* Métodos habilitados (POST, GET, TRACE etc)
