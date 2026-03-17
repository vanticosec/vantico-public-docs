# SQL Injection

## SQL Injection

### Gate 1 — Evidência mínima

O pentester deve submeter com todos os itens abaixo. Sem dado real extraído, a finding é devolvida antes do Gate 2.

* [ ] Parâmetro afetado identificado com payload específico documentado
* [ ] Dado real extraído da base (não apenas mensagem de erro de sintaxe)
* [ ] Screenshot do request e response com a exploração ativa
* [ ] Ferramenta ou método utilizado documentado

***

### Gate 2 — Checklist de profundidade

**Armazenamento de senhas**

* [ ] Senhas em texto plano no banco?
* [ ] Hash sem salt implementado?
* [ ] Algoritmo fraco (MD5, SHA1)?

**Permissões do usuário de banco**

* [ ] Usuário tem acesso a múltiplos databases?
* [ ] Permissão `FILE` habilitada? (leitura de arquivos do servidor)
* [ ] `xp_cmdshell` habilitado no MSSQL? (vetor de RCE)

**Escopo dos dados**

* [ ] Quantos registros são acessíveis?
* [ ] PII presente? (CPF, e-mail, telefone, dados financeiros)
* [ ] Dados de saúde ou financeiros? (agrava enquadramento LGPD)

**Encadeamento**

* [ ] É possível escalar para RCE?
* [ ] Credenciais obtidas funcionam em outros serviços?

***

### Encadeamentos possíveis

* RCE via `xp_cmdshell` (MSSQL)
* Leitura de arquivos do servidor via permissão `FILE`
* Dump completo de todos os databases acessíveis
* Escalação de privilégios dentro do banco

***

### Template de impacto para o relatório

> Preencha os campos entre colchetes com os dados reais do engajamento.

SQL Injection no parâmetro `[parâmetro]` do endpoint `[endpoint]` permite manipular diretamente os comandos enviados ao banco `[nome do banco]`.

A exploração permitiu extrair `[N]` registros da tabela `[tabela]`, incluindo `[tipos de dados sensíveis]`. As senhas estão armazenadas `[em texto plano / com hash MD5 sem salt / com bcrypt]`.

O usuário de banco `[db_user]` possui acesso a `[N]` databases além do necessário para o funcionamento da aplicação, violando o princípio de menor privilégio.

No cenário mais grave identificado, é possível `[ação de maior impacto]`.

A vulnerabilidade expõe dados pessoais de `[N]` usuários e configura violação ao Art. 46 da LGPD.

**Recomendação**

1. Utilizar prepared statements em todas as consultas ao banco
2. Aplicar menor privilégio ao usuário de banco
3. Revisar armazenamento de senhas — implementar bcrypt ou Argon2 com salt
4. Revogar permissão `FILE` e desabilitar `xp_cmdshell` se não utilizados
