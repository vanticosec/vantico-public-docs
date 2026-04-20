---
description: >-
  Aplicações que processam transações monetárias requerem atenção especial à
  lógica de validação numérica. Muitos sistemas falham ao lidar com valores fora
  do intervalo esperado.
---

# Aplicações Financeiras

### Manipulação de Valores em Transações

{% hint style="info" %}
Para cada campo que aceita um valor monetário, teste sistematicamente todas as categorias abaixo. Documente o comportamento exato da aplicação para cada input.
{% endhint %}

### Valores extremos

* Inserir valores negativos (`-100.00`), pode gerar crédito indevido
* Inserir zero (`0`ou`0.00`)
* Inserir valores decimais com precisão excessiva (`0.000001`)
* Inserir valores muito grandes (`999999999999.99`), overflow de campo
* Inserir valores muito pequenos (`0.001`)

### Tipos de dados inválidos

* `NaN`— Not a Number
* `Infinity`e`-Infinity`
* `null`— campo omitido ou explicitamente nulo
* Notação científica (`1e10`,`1.5e-3`)
* String no lugar de número (`"cem reais"`)

### Técnicas de manipulação

* Repetir o mesmo parâmetro múltiplas vezes no body, qual valor é usado?
* Omitir parâmetro completamente, qual o valor padrão assumido?
* Usar múltiplos códigos de desconto
* Usar códigos de desconto expirados

```
# Exemplos de payloads para testar em campos monetários
-100
0
0.001
999999999
NaN
Infinity
-Infinity
null
1e10
"amount"

# Repetição de parâmetro (comportamento depende do parser)
amount=100&amount=-100
{"amount": 100, "amount": -100}
```

### Dados de Pagamento

* Dados completos de cartão salvo visíveis no frontend (PAN full, CVV)
* Enumeração de cartão via endpoint de registro, resposta diferente para cartão existente
* Ausência de senha de confirmação em transações de alto valor
* Ausência de 2FA em transferências

{% hint style="warning" %}
Aplicações que processam cartões estão sujeitas ao PCI DSS. A exposição de dados de cartão (PAN, CVV, data de expiração) é violação direta. Reporte com contexto de compliance além do risco técnico.
{% endhint %}
