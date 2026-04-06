---
description: >-
  O serviço da web é o serviço mais comum e extenso e existem vários tipos
  diferentes de vulnerabilidades.
---

# Checklist

**Porta Padrão:** 80 (HTTP), 443 (HTTPS)

<pre><code><strong>PORT     STATE    SERVICE
</strong>80/tcp   open     http
443/tcp  open     ssl/https
</code></pre>

```
nc -v (domínio.com) 80 #GET / HTTP/1.0
openssl s_client -connect (domínio.com):443 #GET / HTTP/1.0
```



**Low Hanging Fruit - Information Gathering**

* [ ] Encontrar LinkedIn
* [ ] Informações Pastebin e Trello
* [ ] Google Hacking, exemplo: ext:, intext: intitle:
* [ ] Metadados em arquivos
* [ ] Shodan / Censys
* [ ] Busca em certificados (crt.sh)
* [ ] Virus Total
* [ ] DnsDumpster
* [ ] SecurityTrails
* [ ] [email-spoof](https://github.com/vanticohq/email-spoof)
* [ ] Subdominios (subfinder, SecurityTrails, DnsDumpster, crt.sh, Amass)
* [ ] Subdomain Takeover
* [ ] Busca robots.txt e sitemap.xml
* [ ] Busca e-mails (hunter.io, anymailfinder, rocketreach)
* [ ] SpiderFoot
* [ ] Wappalyzer



**Low Hanging Fruits - Tools**

* [ ] Executar low hanging fruits
* [ ] Executar low hanging fruits Data Masking & Privacy
* [ ] [Nmap](https://github.com/nmap/nmap)
* [ ] [Nuclei](https://github.com/projectdiscovery/nuclei)
* [ ] [Katana](https://github.com/projectdiscovery/katana)
* [ ] Força bruta no JWT
  * [ ] [Hashcat](https://github.com/hashcat/hashcat)
  * [ ] [John the Ripper](https://github.com/openwall/john)
* [ ] Verificações no JWT
  * [ ] [JWT](https://jwt.io/)
  * [ ] [JWT Pentest Tool](https://github.com/ticofookfook/JWT_PENTEST/)
  * [ ] [JWTLens](https://jwtlens.netlify.app/)
* [ ] [wafw00f](https://github.com/EnableSecurity/wafw00f)
* [ ] [Fuzzuli](https://github.com/musana/fuzzuli)
* [ ] [WPScan](https://github.com/wpscanteam/wpscan)
* [ ] [ffuf](https://github.com/ffuf/ffuf)

### **Low Hanging Fruits - Checklist**

* [ ] Ausência de cabeçalho
* [ ] Uso de cabeçalho depreciado
* [ ] Js.map
* [ ] Integrity
* [ ] SSL/TLS
* [ ] Vulnerabilidade da versão do server
* [ ] Possibilidade de clickjacking
* [ ] Portas abertas
* [ ] Política de senhas permissivas
* [ ] Mensagem de erros
* [ ] Utilizar bibliotecas JavaScript desatualizadas
* [ ] Enumeração de usuários
* [ ] Falsificação de e-mails
* [ ] Sessão antiga não é inválida após o logout
* [ ] Ausência de mecanismo contra força bruta
* [ ] Uso de IDs sequenciais
* [ ] Upload irrestrito de arquivos
* [ ] Upload de arquivos sem limite de tamanho
* [ ] Registro e monitoramento insuficiente de atividades
* [ ] Falta de validação na alteração de dados
* [ ] Validação de input insuficiente
* [ ] Validação de registro de dados pessoais
* [ ] Invalidação do link de redefinição de senha
* [ ] Host header injection
* [ ] Exposição de chaves API
* [ ] Flood de e-mail por meio de redefinição de senha
* [ ] Redirecionamento HTTP para HTTPS
* [ ] Acesso via IP diretamente
* [ ] Aplicação mostrando hash de senhas
* [ ] Páginas do WordPress padrão disponíveis
* [ ] Plugins do WordPress desatualizados
* [ ] Enumeração de usuários via endpoint WordPress
* [ ] Verificações no JWT
* [ ] Negação de serviço com JWT
* [ ] Força bruta na assinatura JWT
* [ ] Página web armazenando credenciais sem criptografia
* [ ] Cookie de sessão sem a flag Secure habilitada
* [ ] Cookie de sessão sem a flag HttpOnly habilitada
* [ ] Cookie com tamanho maior que 4096 bytes
* [ ] Listagem de diretórios
* [ ] Gerenciamento de patch insuficiente
* [ ] Ausência do arquivo robots.txt
* [ ] Ausência de WAF
* [ ] Flood em páginas com brute force
* [ ] Ausência de notifcação por login suspeito
* [ ] Subdomínios apontando para IPs privados
* [ ] CORS Misconfiguration
* [ ] Ausência de segundo fator de autenticação no procedimento de login
* [ ] Falta de e-mail de verificação no processo de registro
* [ ] Invalidação da sessão após troca de senha
* [ ] Exposição de metadados em imagens
* [ ] Roubo de conta através de redefinição de senha
* [ ] Ausência de notificação para redirecionamento externo
* [ ] Verificação se o usuário pode alterar a senha
* [ ] Token de sessão passado via GET
* [ ] Aplicação sem mecanismo de logout

