# Pós Exploração

## Pós Exploração

Confirmar uma vulnerabilidade é o mínimo. O trabalho de pós exploração é demonstrar o que aquela vulnerabilidade permite fazer além da prova inicial — transformando um achado técnico em impacto compreensível para o cliente.

Esta seção define o processo e os critérios de qualidade aplicados pelo QA.

***

### O processo

Todo finding passa por dois gates antes de entrar no relatório.

#### Gate 1 — Evidência mínima

Responsabilidade do pentester. A finding não entra em triagem sem demonstrar exploração real. Os critérios por tipo de vulnerabilidade estão nas subpáginas.

#### Gate 2 — Profundidade

Responsabilidade do QA. Após o Gate 1, o QA verifica se o pentester explorou o impacto encadeado. Se insuficiente, o QA pode:

* Solicitar complemento ao pentester (24h para crítico, 48h para alto)
* Investigar e complementar ele mesmo

***

### Por que aprofundar importa

| Sem pós exploração                  | Com pós exploração                                                                                                           |
| ----------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| "SQLi confirmado no parâmetro id="  | "SQLi expõe 82.000 registros com CPF. Senhas em MD5 sem salt. Usuário de banco acessa 3 databases adicionais."               |
| "XSS stored no campo de comentário" | "XSS stored executa no painel admin. HttpOnly ausente permite roubo de sessão e account takeover de qualquer administrador." |
| "Share SMB acessível anonimamente"  | "Share contém credencial válida em 14 hosts, incluindo o Domain Controller."                                                 |

***

### Subpáginas

* SQL Injection
* XSS Stored
* IDOR / Controle de Acesso
* SSRF
* Secrets expostos
