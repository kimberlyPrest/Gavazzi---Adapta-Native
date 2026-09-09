# Matriz de SPECs — Fase 1

| SPEC | Resultado | Origem | Critérios de aceite | Arquivo |
|---|---|---|---|---|
| SPEC-1-001 | Acesso e papéis | RF-01; RNF autenticação/autorização; CA-1-01/14 | CA-1-001-01, CA-1-001-02, CA-1-001-03, CA-1-001-04, CA-1-001-05, CA-1-001-06, CA-1-001-07, CA-1-001-08, CA-1-001-09, CA-1-001-10, CA-1-001-11, CA-1-001-12, CA-1-001-13, CA-1-001-14 | SPEC-1-001-acesso-e-papeis.md |
| SPEC-1-002 | Cadastro de projetos e disciplinas | RF-01; RN-01; CA-1-02 | CA-1-002-01, CA-1-002-02, CA-1-002-03, CA-1-002-04, CA-1-002-05, CA-1-002-06, CA-1-002-07, CA-1-002-08 | SPEC-1-002-cadastro-de-projetos-e-disciplinas.md |
| SPEC-1-003 | Kanban e fluxo configurável | RF-02; RF-05; RN-03; CA-1-03/08/13 | CA-1-003-01, CA-1-003-02, CA-1-003-03, CA-1-003-04, CA-1-003-05, CA-1-003-06, CA-1-003-07, CA-1-003-08, CA-1-003-09 | SPEC-1-003-kanban-e-fluxo-configuravel.md |
| SPEC-1-004 | Filas prioridades e bloqueios | RF-03; RN-01/02/04; CA-1-05/07 | CA-1-004-01, CA-1-004-02, CA-1-004-03, CA-1-004-04, CA-1-004-05, CA-1-004-06, CA-1-004-07 | SPEC-1-004-filas-prioridades-e-bloqueios.md |
| SPEC-1-005 | Handoffs e recuperação de falhas | RF-04; RF-15; RN-03; CA-1-04/11/12 | CA-1-005-01, CA-1-005-02, CA-1-005-03, CA-1-005-04, CA-1-005-05, CA-1-005-06, CA-1-005-07, CA-1-005-08, CA-1-005-09 | SPEC-1-005-handoffs-e-recuperacao-de-falhas.md |
| SPEC-1-006 | Touch time e baseline em modo sombra | RF-06; RN-14; CA-1-06/09 | CA-1-006-01, CA-1-006-02, CA-1-006-03, CA-1-006-04, CA-1-006-05, CA-1-006-06, CA-1-006-07, CA-1-006-08, CA-1-006-09, CA-1-006-10 | SPEC-1-006-touch-time-e-baseline-em-modo-sombra.md |
| SPEC-1-007 | Painel auditoria adoção e exportação | RF-05; RF-11; CA-1-07/10/15/16 | CA-1-007-01, CA-1-007-02, CA-1-007-03, CA-1-007-04, CA-1-007-05, CA-1-007-06, CA-1-007-07, CA-1-007-08, CA-1-007-09, CA-1-007-10, CA-1-007-11, CA-1-007-12, CA-1-007-13, CA-1-007-14 | SPEC-1-007-painel-auditoria-adocao-e-exportacao.md |

## Cobertura da Fase 1

| Capacidade | SPEC dona | Prova principal |
|---|---|---|
| Acesso, papéis e revogação | SPEC-1-001 | autorização, recuperação, força bruta, sessão e ausência de segredo em logs |
| Cadastro de projeto/disciplinas | SPEC-1-002 | cadastro, responsável, duplicidade, autorização e links seguros |
| Kanban e estados | SPEC-1-003 | fluxo Entrada pendente → Aprovado, critérios de avanço, concorrência e rollback |
| Filas, prioridade e bloqueios | SPEC-1-004 | ordenação estável, bloqueio e reatribuição auditada |
| Handoffs | SPEC-1-005 | idempotência, falha recuperável, notificação persistente e reprocessamento autorizado |
| Touch time e baseline | SPEC-1-006 | modo sombra, importação histórica, timer abandonado e CSV reproduzível |
| Painel, auditoria e adoção | SPEC-1-007 | drill-down, export autorizado, fórmulas, retenção e backup/restauração |

## Estado

- 7 SPECs de produto.
- 71 critérios de aceite únicos.
- Tasks ainda não geradas; seção `Tasks vinculadas` permanece reservada.
- Nenhuma implementação iniciada.
