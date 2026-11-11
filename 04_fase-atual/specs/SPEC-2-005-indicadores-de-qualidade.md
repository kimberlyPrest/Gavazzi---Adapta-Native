# SPEC-2-005 — Indicadores de qualidade (K2 e K3)

**Fase:** 2  
**Status:** planejada  
**Dono:** Tomaz  
**Origem no escopo:** RF-11; K2; K3; indicadores de apoio; CA-2-10  
**Degrau da solução:** construção mínima — cálculo no painel que já existe, com a mesma regra de inconclusivo da Fase 1.

## Resultado observável

O painel mostra quanto do checklist sai conforme na primeira revisão (K2) e quantas correções válidas aparecem depois da emissão (K3), por projeto, disciplina, pessoa e período. Cada número abre os registros que o formaram e bate com a exportação.

## Limites e dependências

- **Inclui:** K2 = itens conformes na 1ª rodada ÷ itens aplicáveis verificados na 1ª rodada (N/A e exceções fora do denominador, mostrados à parte); K3 = correções válidas após a emissão ÷ disciplinas emitidas, separadas por origem e severidade; taxa de retorno para correção (rodadas reprovadas ÷ rodadas); média de rodadas até aprovar, por pessoa; filtros por projeto, disciplina, pessoa, tipologia e período; drill-down; exportação CSV.
- **Fora de escopo:** comparação antes × depois do K1 e metas por pessoa ou pontuação (decisões futuras).
- **Entradas e pré-condições:** rodadas (SPEC-2-003) e emissões/correções (SPEC-2-004).
- **Saídas/artefatos:** cards no painel, drill-down e CSV.
- **Dependências e responsáveis:** Alessandro e Tomaz leem; coordenadores veem a própria equipe; projetista vê só os próprios números.
- **Risco e plano B:** amostra abaixo do limiar (padrão: 5 disciplinas revisadas para K2 e 5 emitidas para K3, configurável) aparece como "inconclusivo", nunca como resultado.
- **Rollback ou reversão:** os indicadores são só leitura; mudar o limiar fica no histórico de configuração.

## Fluxo e regras

1. O usuário abre **Painel › Qualidade** e escolhe os filtros.
2. O sistema calcula K2, K3, taxa de retorno e rodadas médias.
3. Cada número abre a lista de rodadas, itens, emissões ou correções que o formaram.
4. A exportação traz as mesmas linhas.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | 6 disciplinas revisadas, 40 itens aplicáveis, 34 conformes na 1ª rodada | K2 = 85% | — |
| Limite | 3 disciplinas emitidas | K3 "inconclusivo (3 de 5)" | aguardar amostra |
| Falha | projetista filtra outra pessoa | só os próprios dados | — |

## Checklist de execução

- [ ] Conferir o K2 de um projeto com os itens no drill-down.
- [ ] Conferir o K3 com uma correção válida e uma inválida.
- [ ] Exportar o CSV e comparar com o painel.
- [ ] Conferir o "inconclusivo" com amostra pequena.

## Critérios de aceite

- [ ] **CA-2-005-01:** K2 usa só a 1ª rodada; N/A e exceções ficam fora do denominador e aparecem em contagem separada.
- [ ] **CA-2-005-02:** O drill-down do K2 lista as rodadas e itens usados.
- [ ] **CA-2-005-03:** K3 conta só correções válidas após a emissão, separadas por origem e severidade, com drill-down.
- [ ] **CA-2-005-04:** Abaixo do limiar configurado, o indicador aparece como "inconclusivo" com a contagem da amostra.
- [ ] **CA-2-005-05:** Projetista vê só os próprios números; coordenador vê a equipe; admin/diretor e administrativo veem tudo.
- [ ] **CA-2-005-06:** O CSV exportado reproduz exatamente os números do painel com os mesmos filtros.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | fórmula com N/A e 2ª rodada | calcular com fixture conhecida | número errado antes da implementação | log RED |
| GREEN | K2, K3, retorno e rodadas | rodar a fixture de resultado conhecido | 85%, K3 e taxas iguais ao esperado | suíte + captura |
| REFACTOR/REGRESSÃO | limiar, permissão e CSV | amostra 4/5; projetista; exportação | inconclusivo; escopo respeitado; CSV igual | suíte + CSV |

**Dados/fixtures:** 6 disciplinas com 40 itens aplicáveis (34 conformes na 1ª rodada, 3 N/A, 1 exceção), 3 emissões com 2 correções válidas e 1 inválida, 3 pessoas.  
**Caminhos de erro obrigatórios:** amostra pequena, filtro sem dados (estado vazio explícito), acesso fora do escopo.  
**Evidência exigida:** teste da fixture de resultado conhecido e CSV conferido com o painel.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.14 | Implementar K2 (1ª rodada) por projeto, disciplina, pessoa e período, com drill-down | Executor (Maestro) | CA-2-005-01, CA-2-005-02, CA-2-005-05 | TDD GREEN (fórmula K2) | Teste com fixture de resultado conhecido | T2.13 concluída | Planejada |
| T2.15 | Implementar K3, retorno para correção e rodadas por pessoa, inconclusivo e exportação CSV | Executor (Maestro) | CA-2-005-03, CA-2-005-04, CA-2-005-06 | TDD GREEN (K3 e CSV) | CSV conferindo com o painel | T2.14 concluída | Planejada |
| T2.16 | Teste humano da SPEC-2-005 | Alessandro + Tomaz | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas | T2.15 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.14 e T2.15 no ar. T2.16 é este teste.
- **Quem testa:** Alessandro e Tomaz.
- **Passos:** 1) abrir Painel › Qualidade e conferir o K2 de um projeto de teste abrindo o drill-down; 2) conferir o K3 e a taxa de retorno; 3) exportar o CSV e comparar com a tela; 4) conferir que, com poucos projetos, o indicador aparece como inconclusivo.
- **Resultado esperado:** CA-2-005-01 a CA-2-005-04 e CA-2-005-06; o CA-2-005-05 fecha pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas e CSV, e mensagem do Tomaz registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
