# SPEC-2-003 — Revisão, retorno para correção e exceção

**Fase:** 2  
**Status:** planejada  
**Dono:** Coordenadores  
**Origem no escopo:** RF-08; RF-09; RN-07; RN-08; CA-2-06/07  
**Degrau da solução:** construção mínima — rodada de revisão sobre o checklist congelado do card, usando os estados da Fase 1.

## Resultado observável

O coordenador revisa a disciplina item por item. Se algo não está conforme, o card volta para o projetista em "Em correção" com a lista do que corrigir; a segunda rodada fica registrada ao lado da primeira.

## Limites e dependências

- **Inclui:** abrir rodada de revisão no card em "Aguardando revisão"; marcar cada item aplicável; resultado aprovado (nenhum não conforme pendente) ou reprovado; retorno para "Em correção" com itens, motivo e responsável; projetista marca o que corrigiu e reenvia; nova rodada numerada; exceção técnica aceita só por coordenador ou admin/diretor, com justificativa.
- **Fora de escopo:** revisão automática por IA, comentário em arquivo, emissão (SPEC-2-004).
- **Entradas e pré-condições:** checklist de revisão aplicado ao card (SPEC-2-002); coordenador do projeto definido.
- **Saídas/artefatos:** rodadas com resultado por item, histórico e card no estado certo.
- **Dependências e responsáveis:** quem revisa é o coordenador do projeto (regra da SPEC-1-008); admin/diretor também pode.
- **Risco e plano B:** sem checklist de revisão aplicado, a revisão continua possível com resultado geral e motivo, marcada como "sem checklist" (fora do K2).
- **Rollback ou reversão:** reabrir uma rodada encerrada só por coordenador/admin, com justificativa; a versão anterior da rodada fica no histórico.

## Fluxo e regras

1. O projetista conclui e o card vai para "Aguardando revisão".
2. O coordenador abre a rodada 1 e marca os itens.
3. Reprovada: o card volta para "Em correção" com os itens não conformes e o responsável.
4. O projetista corrige, marca os itens corrigidos e reenvia.
5. O coordenador abre a rodada 2. Aprovada: o card vai para "Aprovado".
6. Item não conforme pode virar exceção técnica, com justificativa e quem decidiu.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | 2 itens não conformes na rodada 1 | card em "Em correção" com 2 itens | — |
| Limite | todos conformes ou N/A justificados | aprovado na rodada 1 | — |
| Falha | projetista tenta aprovar ou aceitar exceção | 403 auditado | — |

## Checklist de execução

- [ ] Reprovar uma rodada com 2 itens.
- [ ] Conferir os itens na fila do projetista.
- [ ] Corrigir, reenviar e aprovar na rodada 2.
- [ ] Aceitar 1 item como exceção com justificativa.

## Critérios de aceite

- [ ] **CA-2-003-01:** Só o coordenador do projeto ou admin/diretor abre e encerra rodada de revisão.
- [ ] **CA-2-003-02:** A rodada registra resultado por item, autor, horário e número da rodada.
- [ ] **CA-2-003-03:** Rodada reprovada leva o card para "Em correção" com itens, motivo e responsável visíveis na fila do responsável.
- [ ] **CA-2-003-04:** O projetista marca os itens corrigidos e reenvia; o card volta para "Aguardando revisão".
- [ ] **CA-2-003-05:** A nova rodada preserva as anteriores; o histórico mostra todas, em ordem.
- [ ] **CA-2-003-06:** Exceção técnica exige justificativa e registra quem decidiu; só coordenador e admin/diretor podem aceitar.
- [ ] **CA-2-003-07:** Aprovação com exceção fica marcada como "aprovado com exceção" no card e no histórico.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | aprovação por projetista e exceção sem justificativa | tentar ambos | aceitos antes da implementação | log RED |
| GREEN | rodada reprovada → correção → rodada aprovada | rodar o ciclo completo | estados e histórico corretos | suíte + histórico |
| REFACTOR/REGRESSÃO | reabertura e concorrência | reabrir rodada; dois coordenadores encerrando ao mesmo tempo | reabertura registrada; um só encerramento vale | suíte |

**Dados/fixtures:** card com checklist de revisão de 6 itens (1 crítico), coordenador do projeto, outro coordenador, projetista.  
**Caminhos de erro obrigatórios:** papel sem permissão, exceção sem justificativa, encerramento concorrente, revisão sem checklist.  
**Evidência exigida:** testes do ciclo e histórico com duas rodadas.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.07 | Implementar rodada de revisão pelo coordenador do projeto com resultado aprovado/reprovado e retorno para "Em correção" | Executor (Maestro) | CA-2-003-01..03 | TDD GREEN (rodada e retorno) | Suíte passando + histórico da rodada | T2.06 concluída | Planejada |
| T2.08 | Implementar correção pelo projetista e nova rodada preservando as anteriores | Executor (Maestro) | CA-2-003-04, CA-2-003-05 | TDD GREEN (nova rodada) | Histórico com duas rodadas | T2.07 concluída | Planejada |
| T2.09 | Implementar exceção técnica (coordenador/administrador, justificativa, quem decidiu) | Executor (Maestro) | CA-2-003-06, CA-2-003-07 | TDD RED/GREEN (exceção sem permissão) | Teste de exceção negada + registro da aceita | T2.07 concluída | Planejada |
| T2.10 | Teste humano da SPEC-2-003 | Coordenador + projetista | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas | T2.09 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.07 a T2.09 no ar. T2.10 é este teste.
- **Quem testa:** um coordenador com um projetista, num projeto de teste.
- **Passos:** 1) reprovar a rodada 1 com 2 itens; 2) o projetista confere os itens na fila, corrige e reenvia; 3) aprovar na rodada 2 e conferir as duas rodadas no histórico; 4) em outro card, aceitar um item como exceção com justificativa.
- **Resultado esperado:** CA-2-003-02 a CA-2-003-07; o CA-2-003-01 fecha pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas e mensagem do coordenador registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
