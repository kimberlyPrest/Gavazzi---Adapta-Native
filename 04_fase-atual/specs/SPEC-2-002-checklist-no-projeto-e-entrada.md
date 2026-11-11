# SPEC-2-002 — Checklist aplicado ao projeto e checklist de entrada

**Fase:** 2  
**Status:** planejada  
**Dono:** Coordenadores  
**Origem no escopo:** RF-07; RN-05; RN-06; RN-02; CA-2-03/04/05  
**Degrau da solução:** construção mínima — usa o card de disciplina, o Fluxo e o bloqueio que já existem na Fase 1.

## Resultado observável

Cada disciplina do projeto mostra o checklist certo, na versão que valia quando ele foi aplicado. Item de entrada que falta vira pendência com dono e prazo, e item crítico pendente segura o card antes de "Pronto".

## Limites e dependências

- **Inclui:** em **Administração › Fluxo**, escolher em qual etapa cada tipo de checklist é aplicado (padrão: entrada em "Entrada pendente", revisão em "Aguardando revisão"); aplicar a versão vigente do modelo da disciplina (e da tipologia, se houver), congelada no card; marcação por item: conforme, não conforme ou não se aplica (com justificativa); pendência de entrada com dono e prazo, usando o bloqueio da Fase 1; trava de avanço para "Pronto" enquanto houver item crítico de entrada pendente.
- **Fora de escopo:** rodadas de revisão (SPEC-2-003), leitura automática de arquivos.
- **Entradas e pré-condições:** modelo publicado (SPEC-2-001); projeto com disciplina e responsável.
- **Saídas/artefatos:** checklist do card com histórico de marcações.
- **Dependências e responsáveis:** sem modelo vigente para a disciplina, o card mostra "sem checklist" e não trava nada.
- **Risco e plano B:** se o modelo mudar depois de aplicado, o card continua na versão congelada; trocar de versão só por ação explícita do coordenador, registrada.
- **Rollback ou reversão:** desmarcar um item volta ao estado anterior com registro; o histórico não é apagado.

## Fluxo e regras

1. O card entra na etapa configurada.
2. O sistema aplica a versão vigente do modelo e congela.
3. Projetista ou coordenador marcam os itens.
4. Item de entrada "não conforme" abre pendência (motivo, dono, prazo). Com item crítico pendente, o card não vai para "Pronto".

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | card entra em "Entrada pendente" | checklist de entrada v1 aplicado | — |
| Limite | modelo republicado (v2) depois da aplicação | card continua na v1 | coordenador troca para v2 com registro |
| Falha | mover para "Pronto" com item crítico pendente | movimento recusado com o item indicado | resolver a pendência |

## Checklist de execução

- [ ] Criar projeto com disciplina que tenha modelo de entrada e de revisão.
- [ ] Marcar um item "não se aplica" sem justificativa (deve recusar).
- [ ] Deixar um item crítico pendente e tentar mover para "Pronto".
- [ ] Publicar v2 do modelo e conferir que o card segue na v1.

## Critérios de aceite

- [ ] **CA-2-002-01:** A etapa de aplicação de cada tipo é configurável no Fluxo e entra no histórico de configuração.
- [ ] **CA-2-002-02:** Ao entrar na etapa, o card recebe a versão vigente do modelo da disciplina (e da tipologia, quando houver), uma única vez.
- [ ] **CA-2-002-03:** Nova publicação do modelo não altera checklists já aplicados; troca de versão só por coordenador, registrada.
- [ ] **CA-2-002-04:** Cada item registra resultado, autor e horário; "não se aplica" exige justificativa.
- [ ] **CA-2-002-05:** Item de entrada não conforme cria pendência com motivo, dono e prazo, visível na fila do dono.
- [ ] **CA-2-002-06:** Card com item crítico de entrada pendente não avança para "Pronto"; a mensagem indica qual item.
- [ ] **CA-2-002-07:** Disciplina sem modelo vigente mostra "sem checklist" e não trava o fluxo.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | avanço com item crítico pendente e N/A sem justificativa | tentar ambos | aceitos antes da implementação | log RED |
| GREEN | aplicação, congelamento, marcação e trava | rodar cenários com v1 → v2 | card na v1, trava ativa, pendência na fila | suíte + captura |
| REFACTOR/REGRESSÃO | aplicação repetida e disciplina sem modelo | mover o card ida e volta; disciplina sem modelo | sem checklist duplicado; fluxo livre | suíte |

**Dados/fixtures:** projeto com 2 disciplinas (uma sem modelo), modelo de entrada com 1 item crítico, modelo de revisão, projetista e coordenador.  
**Caminhos de erro obrigatórios:** N/A sem justificativa, avanço travado, reaplicação, troca de versão sem permissão.  
**Evidência exigida:** testes de congelamento e trava e captura do checklist no card.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.04 | Aplicar e congelar a versão vigente do checklist em cada disciplina do projeto, na etapa configurada no Fluxo | Executor (Maestro) | CA-2-002-01..03 | TDD GREEN (aplicação e congelamento) | Teste da versão congelada após nova publicação | T2.03 concluída | Planejada |
| T2.05 | Implementar marcação por item e pendência de entrada que segura o avanço para "Pronto" | Executor (Maestro) | CA-2-002-04..07 | TDD GREEN (entrada e avanço) | Teste de avanço negado + captura da pendência | T2.04 concluída | Planejada |
| T2.06 | Teste humano da SPEC-2-002 | Coordenador + projetista | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas | T2.05 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.04 e T2.05 no ar. T2.06 é este teste.
- **Quem testa:** um coordenador com um projetista.
- **Passos:** 1) criar um projeto e conferir o checklist de entrada no card; 2) marcar um item como não conforme e conferir a pendência na fila do dono; 3) tentar mover para "Pronto" com um item crítico pendente; 4) resolver e mover; 5) publicar uma versão nova do modelo e conferir que o card não mudou.
- **Resultado esperado:** CA-2-002-02 a CA-2-002-06; o CA-2-002-01 e o CA-2-002-07 fecham pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas e mensagem do coordenador registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
