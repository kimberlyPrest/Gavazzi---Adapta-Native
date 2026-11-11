# Matriz de SPECs — Fase 2

| SPEC | Resultado | Origem | Critérios de aceite | Arquivo |
|---|---|---|---|---|
| SPEC-2-001 | Modelos de checklist configuráveis pela interface | RF-07; RN-05/10; CA-2-01/02; decisão 11/11 | CA-2-001-01 a CA-2-001-07 | SPEC-2-001-modelos-de-checklist.md |
| SPEC-2-002 | Checklist aplicado ao projeto e checklist de entrada | RF-07; RN-02/05/06; CA-2-03/04/05 | CA-2-002-01 a CA-2-002-07 | SPEC-2-002-checklist-no-projeto-e-entrada.md |
| SPEC-2-003 | Revisão, retorno para correção e exceção | RF-08/09; RN-07/08; CA-2-06/07 | CA-2-003-01 a CA-2-003-07 | SPEC-2-003-revisao-correcao-e-excecao.md |
| SPEC-2-004 | Emissão e correções após a emissão | RF-10; RN-09; K3; CA-2-08/09 | CA-2-004-01 a CA-2-004-06 | SPEC-2-004-emissao-e-correcoes-pos-emissao.md |
| SPEC-2-005 | Indicadores de qualidade (K2 e K3) | RF-11; K2; K3; CA-2-10 | CA-2-005-01 a CA-2-005-06 | SPEC-2-005-indicadores-de-qualidade.md |
| SPEC-2-006 | Pastas padrão no OneDrive | Reunião 06/10; decisão 11/11; RN-12; CA-2-11/12 | CA-2-006-01 a CA-2-006-08 | SPEC-2-006-pastas-padrao-no-onedrive.md |

## Cobertura da Fase 2

| Capacidade | SPEC dona | Prova principal |
|---|---|---|
| Checklists pela interface, com versões | SPEC-2-001 | versão imutável, uma vigente, permissão |
| Checklist no projeto e entrada | SPEC-2-002 | congelamento, N/A justificado, trava antes de "Pronto" |
| Revisão e correção | SPEC-2-003 | rodadas preservadas, retorno com itens, exceção autorizada |
| Emissão e correção pós-emissão | SPEC-2-004 | emissão só com aprovação, ligada à entrega; correção válida vira atividade |
| K2, K3 e apoio | SPEC-2-005 | fixture de resultado conhecido, inconclusivo e CSV igual ao painel |
| Pastas no OneDrive | SPEC-2-006 | criação idempotente, nada apagado/movido, falha recuperável |

## Tasks da Fase 2

| Task | SPEC |
|---|---|
| T2.01–T2.03, T2.22 | SPEC-2-001 |
| T2.04–T2.06 | SPEC-2-002 |
| T2.07–T2.10 | SPEC-2-003 |
| T2.11–T2.13 | SPEC-2-004 |
| T2.14–T2.16 | SPEC-2-005 |
| T2.17–T2.21 | SPEC-2-006 |
| T2.23 | Fase 2 (demonstração final) |
