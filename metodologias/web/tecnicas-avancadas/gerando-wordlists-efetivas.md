# Gerando wordlists efetivas

Cracking senhas é mais uma arte do que uma ciência. A maioria dos usuários está (esperançosamente) além dos dias de uso de senhas comuns encontradas em listas de palavras populares, mas as pessoas ainda são pessoas, e senhas são difíceis. Atualmente, é comum encontrar que os usuários possuem senhas compostas por palavras específicas do setor.

Então, como encontramos as palavras certas?

Este é um guia sobre como criar listas de palavras personalizadas para uso em ataques de força bruta e quebra de senhas.

## O que é quebra de senha

Quebra de senha é o processo de hash de palavras ou combinações fornecidas e compará-las com o hash original. Se os hashes corresponderem, a senha foi quebrada. Isso significa que precisamos fornecer a combinação correta e o tipo de hash para obter uma correspondência. Alguns algoritmos de hash são mais fáceis para sistemas modernos processarem do que outros, o que afetará a quantidade de hashes por segundo que podem ser gerados.

Para hashes mais intensivos (como frases de passe WPA para redes sem fio), percorrer uma grande lista de palavras consome tempo e muitas vezes é ineficaz. Portanto, criar uma lista curta e mais personalizada pode ser uma abordagem melhor.

Vamos supor que extraímos o NTDS de um cliente, que usa hashes NTLM e são fáceis de quebrar. Estamos realizando uma auditoria de senhas para o cliente para ver quantas de suas senhas são "facilmente" quebráveis.

Antes de começarmos, precisamos realizar alguns passos rápidos para preparar a quebra de senhas.

## Listas de Palavras Comuns

Existem literalmente milhares de listas de palavras disponíveis na internet para você baixar. Algumas serão mais eficazes do que outras se você estiver tentando quebrar um hash específico. Mas não as baixe todas cegamente. Algumas delas são extraordinariamente grandes (como quase 100 GB).

As mais comuns são:

* SecLists
* RockYou2021
* Kaonashi
* Ignis-sec
* Mystery List
* Crackstation

Existem muitas listas de palavras muito específicas disponíveis que podem ser incrivelmente úteis, como esta para quebrar senhas WiFi geradas pela NetGear. Se você está tentando quebrar uma senha específica e sabe um pouco sobre o dispositivo, isso pode ser muito útil.

Eu coloco todas as minhas listas de palavras favoritas em uma pasta, ordenadas por tamanho de arquivo. (Vou explicar por que elas começam com 2 um pouco mais tarde)

```
./Wordlists
- ./Favourites
  -- 2.mystery-list.txt
  -- 3.ignis-10M.txt
  -- 4.rockyou.txt
  -- 5.kaonashi.txt
  -- 6.realuniq.lst
  -- 7.rockyou2021.txt
```

## Listas de Palavras Personalizadas

Como mencionei anteriormente, essas listas de palavras comuns, embora ainda extremamente úteis, nem sempre serão eficazes. Então, precisamos ser um pouco criativos. Podemos usar algumas ferramentas ou algum pensamento criativo para criar listas de palavras direcionadas.

Como exemplo, podemos pegar alguns dados JSON, como este que é uma lista de subúrbios australianos. Em seguida, podemos passá-lo pelo `jq` para obter o que precisamos.

```
cat suburbs.json | jq -r '.data[].suburb'
```

Ou podemos refinar ainda mais:

```
cat suburbs.json | jq -r '.data[] | select(.urban_area=="Albury - West") | .suburb'
```

Você pode continuar a alterar a lista conforme desejar, fazendo coisas como remover os espaços entre cada palavra, já que eles tendem a ser incomuns em senhas.

## CeWL

Outra ótima maneira de obter dados relevantes é raspar o site do cliente. Podemos usar o CeWL do digininja para fazer isso por nós.

```
cewl -c -m 5 --lowercase -w cewlwordlist.txt https://www.vantico.com.au
```

Isso vai raspar o site da Vantico para todas as palavras com mais de 5 caracteres e ordená-las de acordo com sua frequência. Isso é ótimo para encontrar palavras específicas do setor e informações-chave sobre o cliente que as pessoas podem usar para senhas.

Obtemos algo que se parece com isto:

```
security, 792
vantico, 486
penetration, 395
testing, 264
about, 252
assessment, 162
strategy, 159
engineering, 153
review, 152
social, 152
touch, 151
compliance, 143
vulnerability, 141
cloud, 139
policy, 136
physical, 134
vulnerabilities, 132
executive, 129
terms, 129
education, 127
there, 127
their, 125
```

Em seguida, queremos limpar um pouco. Afinal, há algumas palavras inúteis lá, como “about”, “terms”, “there” e “their”. Mas passar por toda a lista é cansativo, então pegamos as 200 palavras principais da lista (limpando o contador à medida que avançamos) e seguimos a partir daí:

```
head -n 200 cewlwordlist.txt | sed 's/,\s.*$//' > top_200_cewlwordlist.txt
```

Depois, podemos verificar manualmente as 200 palavras e remover quaisquer que sejam desnecessárias.

## CUPP

A Common User Password Profiler (CUPP) ferramenta de Mebus é uma ótima ferramenta para gerar senhas específicas de usuários, mas também possui vários usos extras.

Ao iniciar uma sessão interativa, você pode seguir os prompts para gerar listas de palavras baseadas nas informações da vítima. Geralmente, é uma boa ideia começar com apenas um pouco de informação (nome e sobrenome), caso contrário, as listas de palavras podem ficar muito grandes, muito rapidamente.

```
cupp -i
```

Também solicitará se você gostaria de adicionar Caracteres Especiais, “Números Aleatórios” e converter caracteres para “modo 1337”. No entanto, essa ferramenta é um pouco antiga, então precisa de um pouco de configuração para ser útil.

Encontre seu arquivo “cupp.cfg”. Se você o instalou via os repositórios do Kali, provavelmente estará em `/etc/cupp.cfg`, mas você pode encontrá-lo usando:

```
locate cupp.cfg
# ou
find / -iname "cupp.cfg"
```

Edite o arquivo de configuração para adicionar anos posteriores (eu adiciono até 2025) e altere as configurações do modo l33t conforme achar necessário. (Eu gosto de `a = @`, `i = !`). Também ajuste a configuração de “Formatação de comprimento de palavra” para acomodar palavras mais longas.

**Nota:** Se você quiser adicionar mais caracteres, precisará editar a própria ferramenta para fazer as substituições extras.

Outra característica legal do CUPP é pegar uma lista de palavras existente (como as que criamos anteriormente) e modificá-las para nós com nossas configurações.

```
cupp -w <wordlist>
```

## Username Anarchy

Uma última ferramenta que vale a pena mencionar é o Username Anarchy de Urban Adventurer. É uma ferramenta simples que pegará uma string e gerará uma lista curta de possíveis nomes de usuário. Como não é incomum encontrar nomes de usuários em senhas, isso pode gerar alguns resultados interessantes. Também é super útil para ataques de força bruta.

```
./username-anarchy Harry Potter > harrypotter.txt
```

## Limpando Nossas Listas de Palavras

Se tivermos informações sobre a política de senhas, podemos usá-las a nosso favor para reduzir nossas listas de palavras. Isso reduz a quantidade de processamento e aumenta nossas chances de sucesso.

Esta é a maneira mais limpa que encontrei para fazer isso. (existem métodos mais eficientes, mas são mais difíceis de ler). Este comando de uma linha encontrará todas as palavras que atendem aos seguintes requisitos:

* Letra maiúscula
* Letra minúscula
* Caractere especial
* Número
* Entre 8-12 caracteres

```
cat rockyou.txt |\
 grep '[[:upper:]]' |\
 grep '[[:lower:]]' |\
 grep '[[:digit:]]' |\
 grep '[[:punct:]]' |\
 grep -E '^.{8,12}$' > wordlist.txt
```

Se você apenas deseja definir um comprimento mínimo de caracteres (12 caracteres neste caso), pode usar:

```
cat rockyou.txt |\
 grep '[[:upper:]]' |\
 grep '[[:lower:]]' |\
 grep '[[:digit:]]' |\
 grep '[[:punct:]]' |\
 grep -Ev '^.{,11}$' > wordlist.txt
```

Você pode ser mais específico também, se necessário:

* Letra maiúscula
* Letra minúscula
* Mais de 20 caracteres
* Um dos seguintes caracteres especiais: $, #, @
* Termina em um dígito

```
cat rockyou.txt |\
 sed -r '/[$#@]+/!d' |\
 sed -r '/^.{,19}$/d' |\
 sed -r '/[0-9]$/!d' |\
 grep '[[:upper:]]' |\
 grep '[[:lower:]]' > wordlist.txt
```

Agora que temos nossas listas de palavras organizadas, podemos usá-las para um ataque de força bruta com sua ferramenta favorita ou quebra de senha offline.

## Quebra de Senha

Agora chegamos aos frutos do nosso trabalho. A própria quebra de senha. Supondo que tenhamos nossa lista de hashes de senha e nossas listas de palavras organizadas, precisamos começar a quebrar.

Vamos fingir que temos privilégios de Administrador de Domínio na rede do nosso cliente e extraímos o NTDS. Vamos realizar uma pequena auditoria de senhas para eles.

## Limpando a Lista de Hashes

Cada um de nossos consultores tem uma preferência diferente de ferramentas. Como tal, eles produzem saídas ligeiramente diferentes que precisam ser limpas antes de serem processadas. Uma dessas ferramentas é o GoSecretsDump, que é rápido, mas pode ser irritante de limpar.

Então, primeiro queremos remover contas de máquina. Podemos tratar dessas mais tarde, se necessário.

```
cat ntds.txt | grep -v "\$:"
```

Em seguida, precisamos remover qualquer coisa que não seja um hash NTLM:

```
grep -v "aes[128|256]" | grep -v "des-cbc" | grep -v "rc4-hmac"
```

E então precisamos remover qualquer coisa que não seja um hash de todo (Isso não é um erro de ortografia. Bem, é, mas a ferramenta produz um erro de ortografia… o que nos ajuda)

```
grep -v "gosecretsdump" | grep -v "Coudln"
```

Por fim, talvez queiramos remover o histórico de senhas, por questão de limpeza durante os testes.

```
grep -Ev "_history[0-9]{1,2}:"
```

Então, o comando completo fica assim:

```
cat ntds.txt |\
 grep -Ev "_history[0-9]{1,2}:" |\
 grep -v "\$:" |\
 grep -v "aes[128|256]" |\
 grep -v "des-cbc" |\
 grep -v "rc4-hmac" |\
 grep -v "gosecretsdump" |\
 grep -v "Coudln" > ntds_clean.txt
```

## Regras

A próxima etapa é decidir em qual conjunto de regras executá-lo, já que as palavras em uma lista de palavras geralmente não são suficientes. Conjuntos de regras maiores são mais eficazes, mas consomem mais tempo, então precisam ser considerados. O Hashcat possui regras integradas, que podem ser encontradas na pasta `./rules`. Algumas, como `leetspeak` e `best64`, podem ser úteis, mas nem sempre.

Você pode baixar conjuntos de regras adicionais da internet. Alguns populares são `Clem9669` e `OneRuleToRuleThemAll` ou a versão atualizada de `OneRuleToRuleThemStill`. Ou, se você estiver se sentindo corajoso, pode criar os seus próprios.

## Sintaxe do Comando

Este é meu comando preferido para quebrar senhas.

```
hashcat -m 1000 /path/to/ntds.txt -r ./rules/OneRuleToRuleThemStill.rule /path/to/wordlists/* -O --loopback
```

Vamos detalhá-lo:

* `-m 1000` - Modo 1000 (NTLM). Uma lista de modos pode ser encontrada [aqui](https://hashcat.net/wiki/doku.php?id=hashcat).
* `/path/to/ntds.txt` - um arquivo de texto contendo os hashes de senha.
* `-r ./rules/OneRuleToRuleThemStill.rule` - Usar esta regra para modificar a lista de palavras
* `/path/to/wordlists/*` - Adicionar todas as listas de palavras nesta pasta à Fila de Tentativas (mais sobre isso em um segundo)
* `-O` - Usar kernels otimizados (altera o driver usado pelo Hashcat)
* `--loopback` - Adicionar todas as senhas descobertas a uma lista e, em seguida, passar por essa lista no final reaplicando o mesmo conjunto de regras para encontrar novas senhas.

Ao fornecer um curinga para a lista de palavras, elas serão executadas em ordem alfabética. Por esse motivo, eu começo minha lista de listas de palavras comuns com 2., o que me permite adicionar listas de palavras personalizadas que gostaria de tentar primeiro, anexando-as com 0. ou 1..

Ele continuará trabalhando através de cada lista de palavras, aplicando a função `--loopback` após cada uma, até que a Fila de Tentativas esteja completa.

Também podemos empilhar regras se precisarmos criar diferentes permutações. No entanto, a ordem das regras é importante e criará resultados diferentes.

Uma combinação comum é `-r ./rules/best64.rule -r ./rules/leetspeak.rule`, que fará algumas transformações básicas e, em seguida, aplicará a regra leetspeak sobre essas permutações. No entanto, fazer isso na ordem inversa gera uma lista diferente, que descobri ser menos eficaz.

Outra combinação comum é `-r ./rules/clem9669_case.rule -r ./rules/clem9669_medium.rule`. Isso funciona muito bem, mas é um conjunto muito maior do que a combinação `best64/leetspeak` e, portanto, leva mais tempo. No entanto, mais permutações significam maior chance de sucesso, então faça seu julgamento de acordo.

## Conclusão

Espero que este pequeno guia sobre listas de palavras e quebra de senhas ajude você a encontrar algumas senhas novas e empolgantes. Vou adicionando a ele conforme encontro novos truques.

Boa sorte.
