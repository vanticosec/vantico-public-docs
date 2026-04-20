# Movimentação Lateral

**Tunelamento SSH ou SSH Port Forwarding** é um método para criar uma conexão criptografada (um túnel) entre uma máquina cliente e um servidor permitindo a troca (redirecionamento) das portas de acesso aos serviços.

Esse método é útil para transportar dados de serviços que utilizem protocolos não criptografados, como VNC ou FTP, evitar monitoramento de rede e dar _bypass_ em firewalls.



Como fazer isso com o Putty?



Inicialmente você irá configurá-lo da seguinte maneira:



Em _Session_, você irá adicionar o IP da sua máquina com a porta 22;

<figure><img src="../../../.gitbook/assets/image (9) (1) (1).png" alt=""><figcaption><p>Figura: Session</p></figcaption></figure>



Depois clique em + na parte de SSH e vá em _Tunnels_;

<figure><img src="../../../.gitbook/assets/2024-08-01 10_01_03-PuTTY Configuration.png" alt=""><figcaption><p>Figura: Tunnels</p></figcaption></figure>



Dentro de _Tunnels_, em _Source port_, você irá colocar o seu local host com a porta (ex: 172.0.0.1:1111);

E em _Destination_, o IP que você pretende se conectar com a porta;

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>Figura: Configurações Tunnels</p></figcaption></figure>



Clica em _Open_;

Vai abrir um terminal em que você irá fazer login SSH;

<figure><img src="../../../.gitbook/assets/image (11).png" alt=""><figcaption><p>Figura: Terminal Putty</p></figcaption></figure>



Depois de feito, basta você fazer uma conexão com seu local host, que pode ser feito via _RDP (Remote Desktop Protocol)_ e você já terá concluído seu tunelamento.&#x20;

<figure><img src="../../../.gitbook/assets/2024-08-01 10_20_33-Clipboard.png" alt=""><figcaption><p>Figura: RDP</p></figcaption></figure>

