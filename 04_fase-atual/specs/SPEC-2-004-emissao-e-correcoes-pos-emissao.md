# SPEC-2-004 — Emissão e correções após a emissão

**Fase:** 2  
**Status:** planejada  
**Dono:** Coordenadores  
**Origem no escopo:** RF-10; RN-09; K3; CA-2-08/09  
**Degrau da solução:** construção mínima — liga a revisão aprovada às entregas do calendário que já existem (SPEC-1-008).

## Resultado observável

A emissão de uma disciplina só é registrada depois da revisão aprovada e aparece ligada à entrega do calendário (R00, R01…). Quando chega uma correção depois da emissão, ela fica registrada com origem e severidade e volta para a fila de quem corrige.

## Limites e dependências

- **Inclui:** registrar emissão de disciplina aprovada, com entrega do calendário (tipo prévia, final ou revisão), número da revisão, data, destinatário (texto) e responsável; marcar a entrega como entregue; registrar correção após a emissão com origem (cliente, obra, interna), severidade (alta, média, baixa), descrição, item do checklist opcional e decisão válida/inválida com quem decidiu; correção válida cria atividade em "Em correção" na fila do responsável da disciplina.
- **Fora de escopo:** envio do arquivo ou de e-mail ao cliente, assinatura, ART (os campos de ART da SPEC-1-008 continuam como estão).
- **Entradas e pré-condições:** rodada aprovada (SPEC-2-003); entrega do projeto no calendário.
- **Saídas/artefatos:** emissões e correções que alimentam o K3 (SPEC-2-005).
- **Dependências e responsáveis:** quem registra é o coordenador do projeto ou admin/diretor; o administrativo pode consultar.
- **Risco e plano B:** sem entrega correspondente no calendário, a emissão cria a entrega (tipo e número da revisão) e registra que foi criada na emissão.
- **Rollback ou reversão:** cancelar emissão registrada por engano exige justificativa; a emissão fica marcada como cancelada, não apagada.

## Fluxo e regras

1. A disciplina aprovada mostra o botão **Registrar emissão**.
2. O coordenador escolhe a entrega, o número da revisão e o destinatário.
3. A entrega fica como entregue, com data e responsável.
4. Ao chegar uma correção, o coordenador a registra na emissão; se for válida, o sistema cria a atividade de correção.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | disciplina aprovada + entrega R00 | emissão registrada e entrega marcada | — |
| Limite | correção marcada como inválida | registrada, sem atividade e fora do K3 | coordenador pode revisar a decisão, com registro |
| Falha | emitir disciplina não aprovada | recusado com mensagem | concluir a revisão |

## Checklist de execução

- [ ] Tentar emitir disciplina não aprovada.
- [ ] Emitir R00 de disciplina aprovada.
- [ ] Registrar uma correção válida e uma inválida.
- [ ] Conferir a atividade de correção na fila.

## Critérios de aceite

- [ ] **CA-2-004-01:** Emissão só é possível para disciplina com rodada de revisão aprovada.
- [ ] **CA-2-004-02:** Emissão registra entrega, número da revisão, data, destinatário e responsável, e marca a entrega como entregue.
- [ ] **CA-2-004-03:** Emissão registrada por engano só é cancelada com justificativa e continua no histórico.
- [ ] **CA-2-004-04:** Correção após emissão registra origem, severidade, descrição, item opcional e decisão válida/inválida com quem decidiu.
- [ ] **CA-2-004-05:** Correção válida cria uma atividade de correção na fila do responsável, ligada à emissão.
- [ ] **CA-2-004-06:** Projetista e administrativo não registram emissão nem decidem validade (403 auditado).

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | emissão sem aprovação | registrar emissão em card reprovado | aceita antes da implementação | log RED |
| GREEN | emissão e correção válida/inválida | rodar os três cenários | entrega marcada; atividade só na válida | suíte + captura |
| REFACTOR/REGRESSÃO | cancelamento e entrega inexistente | cancelar emissão; emitir sem entrega | histórico preservado; entrega criada e marcada | suíte |

**Dados/fixtures:** projeto com disciplina aprovada e outra reprovada, entrega R00 no calendário, coordenador, projetista e administrativo.  
**Caminhos de erro obrigatórios:** emissão sem aprovação, papel sem permissão, cancelamento sem justificativa, entrega inexistente.  
**Evidência exigida:** testes de emissão e correção e captura da entrega marcada.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.11 | Implementar registro de emissão ligado à entrega do calendário, só com revisão aprovada | Executor (Maestro) | CA-2-004-01..03 | TDD GREEN (emissão) | Teste de emissão negada sem aprovação + captura | T2.10 concluída | Planejada |
| T2.12 | Implementar correção após emissão com atividade de correção na fila | Executor (Maestro) | CA-2-004-04..06 | TDD GREEN (correção pós-emissão) | Captura da correção + atividade criada | T2.11 concluída | Planejada |
| T2.13 | Teste humano da SPEC-2-004 | Coordenador | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas | T2.12 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.11 e T2.12 no ar. T2.13 é este teste.
- **Quem testa:** um coordenador.
- **Passos:** 1) tentar emitir uma disciplina ainda não aprovada; 2) emitir a R00 de uma aprovada e conferir a entrega no calendário; 3) registrar uma correção válida e conferir a atividade na fila do projetista; 4) registrar uma inválida e conferir que não gera atividade.
- **Resultado esperado:** CA-2-004-01, CA-2-004-02, CA-2-004-04 e CA-2-004-05; o CA-2-004-03 e o CA-2-004-06 fecham pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas e mensagem do coordenador registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
