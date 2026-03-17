# Chaves API

Aplicações que utilizam-se de API para otimizar seu funcionamento, precisam de fornecer essas chaves geradas para que a API funcione corretamente.

Porém muitas vezes essas chaves API (que são um componente que deve ser privado apenas para a aplicação), estão expostas dentro do código fonte e sem nenhum meio de se proteger contra terceiros, o que faz que agentes maliciosos possam se aproveitar delas e utilizá-las.



Para validar uma chave API encontrada há diversos meios variando para qual tipo de API ela funciona, por exemplo:<br>

* Google Maps:

Podemos validar essa chave através do link:

> [https://maps.googleapis.com/maps/api/streetview?size=400x400\&location=40.720032,-73.988354\&fov=90\&heading=235\&pitch=10\&key=TOKEN](https://maps.googleapis.com/maps/api/streetview?size=400x400\&location=40.720032,-73.988354\&fov=90\&heading=235\&pitch=10\&key=TOKEN)

Trocando o campo "TOKEN" pela chave encontrada.



Através da ferramenta Google Maps API Scanner:

> [https://github.com/ozguralp/gmapsapiscanner](https://github.com/ozguralp/gmapsapiscanner)

Executando ela, automaticamente ela testa os parâmetros do Google Maps e retorna uma POC validando o que foi encontrado.



* Slack:

Podemos validar essa chave através do link:

> https://slack.com/api/auth.test?token=xoxp-TOKEN\_HERE\&pretty=1

Trocando o campo "TOKEN" pela chave encontrada.



* Github

Podemos validar essa chave através do link:

> [https://api.github.com/users/whatever?client\_id=xxxx\&client\_secret=yyyy](https://api.github.com/users/whatever?client_id=xxxx\&client_secret=yyyy)

Podemos validar trocando o parâmetro "client\_id" e "client\_secret"



* Gitlab

Podemos validar essa chave através do link:

> [https://gitlab.example.com/api/v4/projects?private\_token=\<your\_access\_token>](https://gitlab.example.com/api/v4/projects?private_token=%3Cyour_access_token%3E)

Podemos validar trocando o parâmetro "your\_acess\_token"



{% hint style="info" %}
Para mais informações, consulte:
{% endhint %}

{% embed url="https://gitlab.com/pentest-tools/PayloadsAllTheThings/-/tree/master/API%20Key%20Leaks" %}

{% embed url="https://github.com/streaak/keyhacks" %}



