# SPEC-1-003 — Kanban e fluxo configurável

**Fase:** 1  
**Status:** planejada  
**Dono:** Tomaz + coordenadores  
**Origem no escopo:** RF-02; RF-05; RN-03; CA-1-03/08/13  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Projetos e disciplinas percorrem um Kanban operacional com estados claros e transições auditadas.

## Limites e dependências

- **Inclui:** estados da Fase 1 Entrada pendente, Pronto, Em elaboração, Aguardando revisão, Em correção e Aprovado; Bloqueado transversal; ordenação; filtros; configuração administrativa de nome/ordem/ativo; regras de transição; critérios configuráveis de avanço limitados a campos obrigatórios da etapa.
- **Fora de escopo:** checklist técnico, automação Revit, emissão documental e desenho de um workflow engine genérico.
- **Entradas e pré-condições:** projetos cadastrados e usuários com papéis.
- **Saídas/artefatos:** Kanban por projeto/disciplina, histórico de transições e configuração reversível.
- **Dependências e responsáveis:** Tomaz configura; coordenadores operam; projetista move Entrada pendente→Pronto→Em elaboração→Aguardando revisão; revisor/coordenador move Aguardando revisão→Em correção/Aprovado; somente coordenador reabre Aprovado com justificativa.
- **Risco e plano B:** fluxo padrão já permite uso sem configuração adicional; ajustes posteriores são versionados.
- **Rollback ou reversão:** restaurar configuração anterior e reverter transição permitida com justificativa.

## Fluxo e regras

1. Usuário abre o Kanban e aplica filtros.
2. Move card para transição permitida.
3. Servidor valida estado, papel e versão.
4. Histórico registra mudança e Kanban atualiza.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | Em elaboração → Aguardando revisão | transição concluída e auditada | — |
| Limite | configuração altera nome/ordem | cards preservam estado e nova versão fica ativa | restaurar versão anterior |
| Falha | Aprovado → Em elaboração por projetista | transição rejeitada | manter estado original; coordenador pode reabrir com justificativa |

## Checklist de execução

- [ ] Criar fluxo padrão e cards de teste.
- [ ] Implementar validação server-side.
- [ ] Testar configuração e restauração.
- [ ] Demonstrar projeto atravessando o fluxo.

## Critérios de aceite

- [ ] **CA-1-003-01:** Kanban mostra todos os estados padrão e cards conforme filtros autorizados.
- [ ] **CA-1-003-02:** Transição válida atualiza o card e registra estado anterior/novo, autor e horário.
- [ ] **CA-1-003-03:** Transição inválida ou concorrente é rejeitada sem sobrescrever estado.
- [ ] **CA-1-003-04:** Bloqueado não substitui o estado principal e exige motivo conforme SPEC-1-004.
- [ ] **CA-1-003-05:** Alterar nome/ordem de etapa não perde cards nem histórico.
- [ ] **CA-1-003-06:** Configuração pode ser restaurada para a versão anterior.
- [ ] **CA-1-003-07:** Um projeto com duas disciplinas percorre o fluxo da Fase 1, de Entrada pendente até Aprovado, em demonstração.
- [ ] **CA-1-003-08:** Somente administrador altera configuração; etapa inativada com cards exige remapeamento explícito e mantém histórico.
- [ ] **CA-1-003-09:** Administrador configura campos obrigatórios por transição; avanço sem esses campos é rejeitado e informa o que falta.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | transição incompatível, papel sem alçada e critério de avanço ausente | tentar mover por API em cada condição | mudança indevida passa antes da entrega | log RED por condição |
| GREEN | Kanban com máquina de estados mínima | rodar testes de transição e fluxo ponta a ponta | válidas passam; inválidas falham; histórico completo | suíte + vídeo |
| REFACTOR/REGRESSÃO | concorrência e reversão de configuração | duas sessões movem o mesmo card; restaurar versão | uma mudança vence explicitamente, outra recebe conflito; rollback preserva cards | logs |

**Dados/fixtures:** 2 projetos, 4 disciplinas, todos os estados e duas versões de configuração.  
**Caminhos de erro obrigatórios:** transição inválida, 403, conflito otimista, etapa inativada e configuração restaurada.  
**Evidência exigida:** vídeo do fluxo, testes de transição e export do histórico.

## Tasks vinculadas

<!-- Preenchida por gerar-tasks após revisão das SPECs. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
