# SPEC-1-004 — Filas prioridades e bloqueios

**Fase:** 1  
**Status:** planejada  
**Dono:** Tomaz + coordenadores  
**Origem no escopo:** RF-03; RN-01/02/04; CA-1-05/07  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Cada pessoa enxerga uma fila acionável de trabalho ordenada por prioridade e prazo, com bloqueios explícitos e responsáveis por resolver.

## Limites e dependências

- **Inclui:** fila individual e por equipe; filtros; prioridade Baixa/Normal/Alta/Urgente; prazo; responsável; bloqueio com motivo, dono, data de revisão; atraso; reatribuição auditada.
- **Fora de escopo:** cálculo de pontos de produtividade, remuneração, escalonamento por IA e notificações externas.
- **Entradas e pré-condições:** cards do fluxo e vínculos de usuários.
- **Saídas/artefatos:** fila ordenada, bloqueios rastreáveis e visão do coordenador.
- **Dependências e responsáveis:** coordenador prioriza/reatribui; responsável atualiza execução; dono do bloqueio resolve.
- **Risco e plano B:** sem regra customizada, ordenar primeiro por bloqueio vencido, depois Urgente→Alta→Normal→Baixa e prazo crescente.
- **Rollback ou reversão:** reatribuição e prioridade podem ser revertidas pelo coordenador com justificativa auditada.

## Fluxo e regras

1. Sistema monta fila com itens atribuídos.
2. Aplica ordem determinística.
3. Usuário abre item e registra bloqueio quando necessário.
4. Coordenador acompanha e reatribui com histórico.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | tarefas com prioridades e prazos distintos | ordem determinística e filtros corretos | — |
| Limite | dois itens com mesma prioridade/prazo | desempate estável por criação/ID | — |
| Falha | bloqueio sem motivo/dono/data | gravação rejeitada | preencher campos obrigatórios |

## Checklist de execução

- [ ] Criar massa com prioridades/prazos variados.
- [ ] Testar ordenação e filtros.
- [ ] Registrar, revisar e resolver bloqueio.
- [ ] Testar reatribuição e auditoria.

## Critérios de aceite

- [ ] **CA-1-004-01:** Fila individual contém somente itens ativos atribuídos ou elegíveis ao usuário.
- [ ] **CA-1-004-02:** Ordenação segue regra padrão e é estável.
- [ ] **CA-1-004-03:** Bloqueio exige motivo, dono e data de revisão.
- [ ] **CA-1-004-04:** Bloqueio vencido é destacado sem mover automaticamente o card.
- [ ] **CA-1-004-05:** Resolver bloqueio registra autor, horário e resolução.
- [ ] **CA-1-004-06:** Mudança de prioridade/responsável registra antes e depois.
- [ ] **CA-1-004-07:** Coordenador visualiza filas da equipe; projetista não vê dados restritos de outra equipe.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | fila sem ordenação e bloqueio permissivo | salvar bloqueio incompleto e comparar ordem esperada | dados inválidos/ordem errada antes da entrega | RED |
| GREEN | fila acionável e bloqueio íntegro | rodar testes de ordenação, filtro e ciclo do bloqueio | todos CAs funcionam | testes + capturas |
| REFACTOR/REGRESSÃO | empate, fuso, atraso e permissão | rodar fixtures de borda e matriz de acesso | ordem estável e sem vazamento | relatório |

**Dados/fixtures:** 12 itens distribuídos entre 3 usuários, prioridades, prazos, dois bloqueios e um atraso.  
**Caminhos de erro obrigatórios:** campos ausentes, prazo/fuso, empate, item arquivado e acesso de outra equipe.  
**Evidência exigida:** capturas das filas, respostas de API e histórico de bloqueios.

## Tasks vinculadas

<!-- Preenchida por gerar-tasks após revisão das SPECs. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
