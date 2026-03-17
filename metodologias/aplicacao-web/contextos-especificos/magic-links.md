---
description: >-
  Links de acesso sem senha, cada vez mais comuns em SaaS e ferramentas
  internas. A segurança depende inteiramente da entropia e validade do token.
---

# Magic Links

### Qualidade do Token

* Verificar se o token é criptograficamente aleatório (deve ter ≥ 128 bits de entropia)Crítico
* Verificar se o token segue algum padrão previsível (timestamp + userId, hash MD5 do e-mail)Crítico
* Analisar múltiplos tokens gerados — há correlação entre eles?

### Validade e Uso

* Testar se o magic link pode ser usado mais de uma vezAlto
* Testar se o magic link funciona após logout do usuárioMédio
* Verificar tempo de validade — ideal entre 5 e 15 minutosMédio
* Testar validade após mudança de fuso horário ou manipulação do relógioBaixo
* Verificar se o link funciona via HTTP (deveria ser HTTPS apenas)

### Enumeração e Leakage

* Troca de parâmetros no link (`user_id`,`email`,`account_id`) — acesso de outro usuárioAlto
* Enumeração de usuários na geração do link — resposta diferente para e-mail inexistenteMédio
* Enumeração por tempo de resposta (timing attack na geração)Médio
* Token aparece na URL — fica exposto em logs do servidor, Referer headers e histórico do browserAlto
* Token aparece no header`Referer`ao navegar para outro site após o login

### Rate Limiting

* Rate limit na geração do link — possível flood de e-mailsMédio
* Geração em massa causa DoS por e-mail na caixa do usuário

{% hint style="info" %}
Ao encontrar token de uso múltiplo ou sem expiração, demonstre o impacto: gere um link, use uma vez, use novamente 30 minutos depois. O screenshot da segunda autenticação bem-sucedida é evidência suficiente.
{% endhint %}
