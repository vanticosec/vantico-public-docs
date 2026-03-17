# Password Spray

Ao contrário do brute force tradicional, em que é testado diversas senhas em um curto período de tempo, no password spray o atacante inverte este lógica, em vez de testar milhares de senhas contra uma única conta, testa menos senhas e rotacionando os usuários testados a cada vez, assim evitando bloqueios automáticos e gerando menos ruído de log do que o brute force tradicional.

Comumente utilizado em portais de login, como da Microsoft 365, VPN, Webmail.

É caracterizado no MITRE ATT\&CK como uma subcategoria do Brute Force: [T1110.003](https://attack.mitre.org/techniques/T1110/003/)



### Ferramentas

As ferramentas comumente utilizadas são:

> [**NetExec**](https://github.com/Pennyw0rth/NetExec)

Utilizada principalmente para realização de password spray em SMB, porém com suporte para outros tipos de protocolos.

```
nxc smb (host) -u /usuarios.txt -p /senhas.txt --no-bruteforce --continue-on-success
```



> [**TREVORspray**](https://github.com/blacklanternsecurity/TREVORspray)

Possui diversos módulos para spray, como para Office 365, Active Directory Federation Services, Outlook Web App, Okta SSO, Cisco VPN.

```
trevorspray -u emails.txt -p 'Senha123' --url https://alvo.com.br
```



> [**0365spray**](https://github.com/0xZDH/o365spray)

Ferramenta específica para enumeração e password spray em Office 365.

```
o365spray --spray -U usuarios.txt -P senhas.txt --count 2 --lockout 5 --domain alvo.com.br
```



> [**Kerbrute**](https://github.com/ropnop/kerbrute)

Ferramenta focada no protocolo Kerberos.

```
./kerbrute_linux_amd64 passwordspray -d dominio.com [--dc (IP)] usuarios.txt Senha123
```



{% hint style="info" %}
Para criar wordlists mais efetivas para realização do password spray, você pode consultar:

[Gerando wordlists efetivas](gerando-wordlists-efetivas.md)
{% endhint %}
