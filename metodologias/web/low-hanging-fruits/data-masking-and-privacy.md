# Data Masking & Privacy

#### **Incosistência de mascaramento entre telas**

Validar se o mascaramento presente em uma tela, permanece o mesmo em outra tela da aplicação.

***

#### **Padrão de mascaramento previsível**

Usar mascaramentos com padrões, permite ataques de força bruta naquele contexto, ou seja, caso seja mascarado como no exemplo a seguir:

```
jo**@gm***.com
```

Ainda assim, podemos fazer ataques de força bruta para descobrirmos este e-mail.

***

#### Mascaramento apenas no frontend

Em alguns casos essa camuflagem pode ser implementada apenas no frontend, o que não impede de ser visualizado os dados em texto plano no backend, como em um chamada da API por exemplo.

```
{
    "cpf":"12345678901",
    "cpf_masked"="123.***.789-**"
}
```

***

#### Vazamento em parâmetros

Em algumas requisições pode ocorrer de chamar através de parâmetros, dados antes mascarados em outra tela.

```
GET /user/?cpf=12345678901
```

***

#### Dados em texto plano em logs

Pode ocorrer dos dados estarem mascarados na UI, porém nos logs estarem em texto plano.

***

#### Exportações sem mascaramento

Em casos onde é possível exportar aquelas informações para formatos como CSV, XLSX, PDF, DOCX, pode ser possível de que o dado exportado venha em formato de texto plano.

***

#### Mascaramento por permissionamento

Deve ser validado se com diferentes permissionamentos, o mascaramento presente é o mesmo.

***

#### Falta de mascaramento em ambientes não produtivos

Deve ocorrer uma validação em ambientes como homologação, a fim de validar se o mascaramento permanece disponível como no ambiente produtivo.

***

#### Quebra de mascaramento via manipulação de parâmetros

Em rotas de API, o fuzzing de parâmetros pode auxiliar para realizar a quebra do mascaramento, auxiliando a identificar parâmetros que removem o mascaramento, como:

```
GET /user/?id=1&view=full

GET /user/?id=1&mask=false

GET /user/?id=1&display=raw

GET /user/?id=1&showSensitiveData=true
```

***

#### Dados expostos em elementos do frontend

Os dados podem ser encontrados sem nenhum tipo de mascaramentos em alguns elementos do frontend, como:

* Comentários HTML
* Variáveis JavaScript
* Source map

Exemplo:

```
<div data-cpf="12345678901">
```

***

#### Falta de mascaramento em ID

O formato de alguns IDs podem expor dados sensíves, como por exemplo:

```
user_pentest_12345678901
```

Pode aparecer dessa maneira também em hashes reversíveis como em base64.
