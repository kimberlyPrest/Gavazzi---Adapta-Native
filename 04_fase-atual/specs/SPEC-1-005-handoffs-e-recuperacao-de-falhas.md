# SPEC-1-005 — Handoffs e recuperação de falhas

**Fase:** 1  
**Status:** planejada  
**Dono:** Coordenadores  
**Origem no escopo:** RF-04; RF-15; RN-03; CA-1-04/11/12  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Concluir uma etapa cria exatamente uma pendência na fila do próximo responsável, sem depender de mensagem manual e sem duplicar em reprocessamento.

## Limites e dependências

- **Inclui:** handoff por transição; criação idempotente da próxima atividade; caixa de eventos/falhas; reprocessamento restrito a coordenador/administrador; confirmação de recebimento; histórico; notificação interna persistente com estado lida/não lida.
- **Fora de escopo:** e-mail, WhatsApp, Telegram, Teams, integrações externas e automação técnica.
- **Entradas e pré-condições:** fluxo ativo, próximo responsável definido ou regra de fallback ao coordenador.
- **Saídas/artefatos:** atividade seguinte, evento de handoff e fila de falhas recuperável.
- **Dependências e responsáveis:** coordenador define responsáveis no projeto; sistema usa fallback ao coordenador quando destino estiver ausente.
- **Risco e plano B:** falha de notificação nunca perde a atividade; ela aparece na caixa de falhas e pode ser reprocessada.
- **Rollback ou reversão:** cancelar handoff não iniciado ou devolver ao estado anterior com justificativa, preservando eventos.

## Fluxo e regras

1. Responsável conclui a etapa.
2. Transação valida e registra a transição.
3. Sistema cria atividade seguinte com chave idempotente.
4. Fila e histórico são atualizados; falha fica visível.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | etapa com próximo responsável | uma atividade criada na fila destino | — |
| Limite | mesmo evento reenviado | nenhuma duplicata | retornar resultado idempotente |
| Falha | destino ausente ou erro de entrega | atividade vai ao coordenador/caixa de falhas | corrigir destino e reprocessar |

## Checklist de execução

- [ ] Criar fluxo com dois responsáveis.
- [ ] Simular sucesso, repetição e falha.
- [ ] Reprocessar evento.
- [ ] Conferir atividade, histórico e ausência de duplicata.

## Critérios de aceite

- [ ] **CA-1-005-01:** Concluir etapa cria uma única atividade seguinte e vínculo ao projeto/disciplina.
- [ ] **CA-1-005-02:** Repetir a mesma requisição/evento não cria duplicata.
- [ ] **CA-1-005-03:** Destino ausente encaminha a pendência ao coordenador e marca necessidade de ajuste.
- [ ] **CA-1-005-04:** Falha é visível com motivo, tentativas e próxima ação.
- [ ] **CA-1-005-05:** Reprocessamento após correção cria/entrega a atividade sem perder histórico.
- [ ] **CA-1-005-06:** Duas conclusões concorrentes não geram duas atividades.
- [ ] **CA-1-005-07:** Cancelamento/devolução exige justificativa e não apaga eventos anteriores.
- [ ] **CA-1-005-08:** Notificação interna aparece como não lida para o destinatário, abre a atividade correta e registra leitura.
- [ ] **CA-1-005-09:** Reprocessamento é restrito a coordenador/administrador e registra autor, horário, tentativa e resultado.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | duplicação e perda de handoff | disparar evento duas vezes e simular erro entre transição/criação | duplicata ou perda ocorre antes da entrega | log RED |
| GREEN | handoff, notificação persistente e reprocessamento autorizado | rodar sucesso, leitura da notificação, duplicação, falha e reprocessamento por papéis | uma atividade, notificação não lida→lida e falha recuperável sem duplicata | suíte + banco + captura |
| REFACTOR/REGRESSÃO | concorrência, retry e rollback | disparar paralelo, reprocessar e devolver | sem duplicata, evento rastreável | trace/log |

**Dados/fixtures:** projeto com duas disciplinas, três etapas, evento repetido, notificação não lida/lida, destino ausente, usuário projetista e coordenador, e falha simulada.  
**Caminhos de erro obrigatórios:** destino ausente, timeout, repetição, concorrência, falha parcial e devolução.  
**Evidência exigida:** testes de idempotência, captura da fila de falhas e histórico completo.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T1.21 | Implementar handoff por transição com criação idempotente da próxima atividade e fallback ao coordenador | Executor (Maestro) | CA-1-005-01, CA-1-005-02, CA-1-005-03, CA-1-005-06 | TDD GREEN da SPEC-1-005 (handoff e idempotência) | Testes de duplicação/concorrência sem duplicata | T1.20 concluída | Planejada |
| T1.22 | Implementar caixa de falhas visível com motivo/tentativas e reprocessamento restrito a coordenador/administrador | Executor (Maestro) | CA-1-005-04, CA-1-005-05, CA-1-005-09 | TDD GREEN da SPEC-1-005 (falha e reprocessamento) | Captura da fila de falhas + log de reprocessamento | T1.21 concluída | Planejada |
| T1.23 | Implementar notificação interna persistente (não lida → lida) vinculada à atividade correta | Executor (Maestro) | CA-1-005-08 | TDD GREEN da SPEC-1-005 (notificação) | Teste de leitura registrada + captura | T1.21 concluída | Planejada |
| T1.24 | Implementar cancelamento/devolução de handoff com justificativa preservando eventos | Executor (Maestro) | CA-1-005-07 | TDD REFACTOR/REGRESSÃO da SPEC-1-005 (rollback) | Histórico íntegro após devolução | T1.22 concluída | Planejada |
| T1.25 | Teste humano da SPEC-1-005: simular sucesso, repetição, falha e reprocessamento no fluxo real | Coordenador | Checklist de execução da SPEC-1-005 | Testes de idempotência + captura da fila de falhas | Checklist assinado | T1.24 concluída | Planejada |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|