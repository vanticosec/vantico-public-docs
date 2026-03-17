---
description: >-
  Aplicações de e-commerce e marketplaces têm uma superfície de lógica de
  negócio extremamente rica. Vulnerabilidades aqui têm impacto financeiro direto
  e mensurável.
---

# Checkout & Pagamentos

{% hint style="danger" %}
Confirme com o cliente se há um ambiente de staging com gateway de pagamento em modo sandbox. Nunca execute testes de manipulação de checkout em produção real.
{% endhint %}

### Manipulação de Preço

* Alterar o valor do campo`price`,`total`ou`amount`diretamente no body da requisição
* Verificar diferença entre valor exibido no front-end e valor cobrado no back-end
* Verificar se o preço final é calculado no client-side (JavaScript)
* Alterar variáveis via DevTools (`cart.total = 0.01`)
* Interceptar response do servidor e alterar valores antes do processamento

```
# Exemplo: alterar price no body
POST /api/checkout
{
  "items": [{"id": "prod_123", "qty": 1}],
  "price": 0.01,  ← alterar aqui
  "total": 0.01
}
```

### Gateway de Pagamento

* Manipular parâmetros em redirects para gateways (PayPal, Stripe, Mercado Pago)
* Forjar callbacks/webhooks com`"status": "paid"`
* Reutilizar o mesmo token de pagamento para múltiplas compras
* Verificar se webhook valida assinatura criptográfica (ex: Stripe-Signature)

### Abuso de Cupons

* Tentar aplicar múltiplos cupons simultaneamente
* Reutilizar cupom de uso único — race condition com requisições paralelas
* Brute-force de códigos promocionais simples (3-6 dígitos numéricos)
* Manipular valor do cupom se ele se reflete em parâmetro da requisição
* Usar cupons expirados

```
# Race condition com Turbo Intruder (Burp)
# Envia N requests simultâneos para o mesmo endpoint
engine.queue(target.req, wordlist)
engine.start(concurrentConnections=50)
```

### Estoque e Quantidade

* Fazer compras simultâneas de item com estoque limitado (race condition)
* Bypass de limite de quantidade mínima/máxima
* Testar compra com estoque zerado (`"qty": 0`ou negativo)
* Adicionar item grátis, remover item elegível e tentar finalizar
* Alterar quantidade de brindes (`"qty": 100`)

### Frete e Endereço

* Inserir CEP no início do checkout, alterar para outro CEP na finalização — preço muda?
* Alterar país/CEP para frete menor após cálculo
* Inserir caracteres Unicode ou scripts em campos de endereço

### Reembolso

* Solicitar reembolso após alterar dados da compra
* Tentar reembolso múltiplo via race condition
* Simular devolução maior que a quantidade comprada
