# SPEC-1-007 — Painel auditoria adoção e exportação

**Fase:** 1  
**Status:** planejada  
**Dono:** Alessandro + Tomaz  
**Origem no escopo:** RF-05; RF-11; CA-1-07/10/15/16  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Alessandro e Tomaz acompanham projetos, atrasos, bloqueios, carga, tempos e completude dos registros em um painel auditável e exportável.

## Limites e dependências

- **Inclui:** cards executivos; filtros por período, projeto, disciplina, etapa e responsável; atrasos/bloqueios; touch time; completude; adoção; export CSV autorizado e auditado; log append-only consultável por administrador e coordenador no seu escopo; retenção de auditoria por 24 meses; backup criptografado, restauração testada e retenção operacional de 90 dias; chave de backup armazenada em secret externo ao banco e acessível somente ao administrador técnico.
- **Fora de escopo:** ranking de pessoas, remuneração, previsão por IA, K2/K3 finais e BI externo.
- **Entradas e pré-condições:** dados das SPECs 001–006; papéis autorizados.
- **Saídas/artefatos:** painel, relatórios, export e evidência de backup/restauração.
- **Dependências e responsáveis:** Executivo consulta agregados sem exportar dados individuais; administrador exporta; coordenador exporta somente sua equipe; toda exportação é auditada com autor, filtros, horário e volume.
- **Risco e plano B:** indicador sem dado suficiente mostra “sem dados/inconclusivo”, nunca zero; export é fonte de reconciliação.
- **Rollback ou reversão:** filtros são descartáveis; restauração recupera dados em ambiente de teste sem sobrescrever produção.

## Fluxo e regras

1. Usuário autorizado abre painel.
2. Aplica filtros e abre drill-down até registros origem.
3. Exporta o mesmo recorte.
4. Consulta auditoria e evidência de backup/restauração.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | dados completos em período | cards e export reconciliam | — |
| Limite | período sem dados | estado vazio explícito | não mostrar zero enganoso |
| Falha | consulta/export grande ou backup falha | erro controlado sem dados parciais | reduzir período/reprocessar e registrar |

## Checklist de execução

- [ ] Popular massa integrada das seis SPECs.
- [ ] Conferir fórmulas e permissões.
- [ ] Comparar painel×CSV.
- [ ] Executar restauração em ambiente de teste.

## Critérios de aceite

- [ ] **CA-1-007-01:** Painel exibe projetos por etapa, prazo, bloqueio e responsável conforme permissões.
- [ ] **CA-1-007-02:** Cada métrica permite chegar aos registros que a compõem.
- [ ] **CA-1-007-03:** Período sem dados mostra estado vazio/inconclusivo.
- [ ] **CA-1-007-04:** Export CSV contém o mesmo conjunto filtrado e totais reconciliam.
- [ ] **CA-1-007-05:** Completude mostra proporção de etapas/itens com apontamentos obrigatórios.
- [ ] **CA-1-007-06:** Adoção mostra usuários ativos e registros por papel sem ranking punitivo.
- [ ] **CA-1-007-07:** Auditoria permite filtrar mudanças de estado, prioridade, responsável e tempo.
- [ ] **CA-1-007-08:** Backup é criado e restauração é demonstrada em ambiente isolado.
- [ ] **CA-1-007-09:** Executivo não altera dados pelo painel.
- [ ] **CA-1-007-10:** Exportação individual é permitida somente a administrador e coordenador no escopo da equipe e é auditada.
- [ ] **CA-1-007-11:** Log é append-only, consultável conforme papel e retido por 24 meses.
- [ ] **CA-1-007-12:** Backup é criptografado, retido por 90 dias e restaurado isoladamente; a chave fica em secret externo ao banco, acessível somente ao administrador técnico.
- [ ] **CA-1-007-13:** Completude = registros obrigatórios preenchidos ÷ esperados; adoção = usuários com ao menos uma criação, transição, bloqueio, handoff ou apontamento válido no período ÷ usuários ativos vinculados a projetos no período, segmentados por papel.
- [ ] **CA-1-007-14:** Abaixo de 80% de completude ou 80% de adoção, métricas dependentes são marcadas inconclusivas.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | métricas, limiar, exportação e auditoria inseguros | comparar consulta/painel/CSV entre papéis, fixture 79%/80% e tentar alterar log/chave | divergência, conclusão indevida ou acesso/alteração passa antes da entrega | RED por cenário |
| GREEN | painel com fórmulas, limiar, export e auditoria protegidos | rodar CA-1-007-01..14 com fixtures 79% e 80% | 79% fica inconclusivo, 80% conclusivo, CSV reconcilia e controles passam | suíte + capturas + CSV |
| REFACTOR/REGRESSÃO | vazio, volume, timezone e restore | testar sem dados, massa grande e restauração isolada | sem zero enganoso, timeout controlado e restore íntegro | relatório de regressão |

**Dados/fixtures:** 12 projetos, 5 papéis, estados, bloqueios, atrasos, tempos completos/incompletos, usuários com atualização válida, cenários de 79% e 80%, e período vazio.  
**Caminhos de erro obrigatórios:** período vazio, fuso, filtro combinado, timeout, export interrompido, acesso proibido, tentativa de export executivo, adulteração de log, backup vencido e falha de restauração.  
**Evidência exigida:** capturas, CSV reconciliado, logs de auditoria e relatório de restauração.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T1.32 | Implementar painel executivo com cards, filtros e drill-down até os registros origem | Executor (Maestro) | CA-1-007-01, CA-1-007-02, CA-1-007-03 | TDD GREEN da SPEC-1-007 (painel e drill-down) | Captura do painel + estado vazio explícito | T1.31 concluída | Planejada |
| T1.33 | Implementar fórmulas de completude e adoção com limiar 80% e marcação de inconclusivo | Executor (Maestro) | CA-1-007-05, CA-1-007-06, CA-1-007-13, CA-1-007-14 | TDD GREEN da SPEC-1-007 (fixtures 79%/80%) | Teste 79% inconclusivo / 80% conclusivo | T1.32 concluída | Planejada |
| T1.34 | Implementar export CSV autorizado e auditado (admin/coordenador no escopo) reconciliando com o painel | Executor (Maestro) | CA-1-007-04, CA-1-007-10 | TDD GREEN da SPEC-1-007 (export e auditoria) | CSV reconciliado + log de exportação | T1.33 concluída | Planejada |
| T1.35 | Implementar log append-only consultável por papel com retenção de 24 meses | Executor (Maestro) | CA-1-007-07, CA-1-007-11 | TDD RED/GREEN da SPEC-1-007 (adulteração de log) | Tentativa de alteração negada + política de retenção | T1.32 concluída | Planejada |
| T1.36 | Implementar backup criptografado com chave em secret externo, retenção de 90 dias e restauração isolada | Executor (Maestro) | CA-1-007-08, CA-1-007-12 | TDD REFACTOR/REGRESSÃO da SPEC-1-007 (restore) | Relatório de restauração em ambiente isolado | T1.35 concluída | Planejada |
| T1.37 | Garantir que executivo não altera dados pelo painel (somente leitura) | Executor (Maestro) | CA-1-007-09 | TDD RED da SPEC-1-007 (tentativa de export/alteração executivo) | Tentativa negada e auditada | T1.33 concluída | Planejada |
| T1.38 | Teste humano da SPEC-1-007: conferir painel×CSV, filtros e evidência de backup/restauração | Alessandro + Tomaz | Checklist de execução da SPEC-1-007 | Capturas + CSV reconciliado + relatório de restore | Checklist assinado | T1.36 e T1.37 concluídas | Planejada |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|