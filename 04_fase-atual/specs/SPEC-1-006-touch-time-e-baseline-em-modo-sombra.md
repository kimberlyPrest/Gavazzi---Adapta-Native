# SPEC-1-006 — Touch time e baseline em modo sombra

**Fase:** 1  
**Status:** planejada  
**Dono:** Kim + Tomaz  
**Origem no escopo:** RF-06; RN-14; CA-1-06/09  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

A Central mede touch time por etapa e registra uma linha de base “antes” separada dos dados do novo fluxo, com exportação reproduzível.

## Limites e dependências

- **Inclui:** iniciar/pausar/encerrar apontamento; encerramento de timer aberto por mais de 12 horas como pendência de revisão; um temporizador ativo por usuário; edição justificada; marca antes/depois; importação CSV histórica com origem/qualidade; amostra; exclusões justificadas; export CSV; cálculo agregado.
- **Fora de escopo:** folha de ponto, produtividade remuneratória, vigilância individual, meta automática e inferência causal.
- **Entradas e pré-condições:** projetos piloto cadastrados; protocolo padrão: elaboração e revisão como touch time, esperas separadas, mínimo de 5 projetos comparáveis quando disponíveis; CSV histórico opcional com projeto, disciplina, tipologia, duração e fonte.
- **Saídas/artefatos:** eventos de tempo auditáveis, dataset baseline, resumo e CSV.
- **Dependências e responsáveis:** projetistas apontam; coordenadores corrigem com justificativa; Kim consulta/exporta.
- **Risco e plano B:** se não houver amostra suficiente, sistema entrega dados e marca baseline inconclusivo; nunca usa 10h estimadas como medição.
- **Rollback ou reversão:** correção gera nova versão/ajuste compensatório; evento bruto original permanece.

## Fluxo e regras

1. Usuário importa histórico validado ou inicia tempo em uma etapa.
2. Pausa/encerra ao interromper ou concluir.
3. Sistema classifica evento como antes/depois e separa espera.
4. Painel agrega e exporta com protocolo.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | sessão válida em elaboração | duração computada e vinculada | — |
| Limite | usuário tenta iniciar segundo timer | ação rejeitada ou encerra anterior com confirmação | sem sobreposição silenciosa |
| Falha | evento negativo/fora do projeto | rejeitado e auditado | corrigir com justificativa |

## Checklist de execução

- [ ] Criar projetos antes/depois e eventos de tempo.
- [ ] Testar timer, pausa e conflito.
- [ ] Gerar baseline e cenário inconclusivo.
- [ ] Comparar cálculo da UI com CSV.

## Critérios de aceite

- [ ] **CA-1-006-01:** Usuário não possui dois temporizadores ativos simultâneos.
- [ ] **CA-1-006-02:** Eventos guardam projeto, disciplina, etapa, usuário, início, fim e marca antes/depois.
- [ ] **CA-1-006-03:** Espera não é somada ao touch time de elaboração/revisão.
- [ ] **CA-1-006-04:** Correção exige motivo e preserva evento original.
- [ ] **CA-1-006-05:** Dados do novo fluxo não entram no grupo “antes”.
- [ ] **CA-1-006-06:** Amostra insuficiente é exibida como inconclusiva.
- [ ] **CA-1-006-07:** CSV reproduz totais e filtros mostrados no painel.
- [ ] **CA-1-006-08:** Nenhum indicador individual é apresentado como avaliação de desempenho nesta fase.
- [ ] **CA-1-006-09:** Importação histórica rejeita linha inválida, informa erros por linha e preserva origem/arquivo/data do dado aceito.
- [ ] **CA-1-006-10:** Timer aberto por mais de 12 horas vira pendência e não entra no baseline até revisão humana.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | timer sobreposto/abandonado, linha histórica inválida e baseline contaminado | criar timer >12h, importar linha inválida e misturar antes/depois | timer pendente entra no cálculo, erro por linha não aparece ou grupos se misturam antes da entrega | RED por cenário |
| GREEN | timer, importação por linha e agregação reproduzíveis | rodar CA-1-006-01..10 e comparar painel/CSV | inválida é rejeitada, timer >12h fica fora do baseline até revisão e CSV confere | suíte + planilha + relatório de importação |
| REFACTOR/REGRESSÃO | fuso, pausa, edição e amostra insuficiente | rodar fixtures de borda e recalcular | sem duração negativa/duplicada; inconclusivo correto | relatório |

**Dados/fixtures:** CSV com 5 projetos históricos “antes”, 2 projetos em modo sombra, eventos de elaboração/revisão/espera, uma linha inválida, fuso de Brasília e uma correção.  
**Caminhos de erro obrigatórios:** sobreposição, timer abandonado, linha inválida de importação, relógio invertido, fuso, edição, exclusão e amostra insuficiente.  
**Evidência exigida:** CSV, cálculo independente e vídeo do apontamento.

## Tasks vinculadas

<!-- Preenchida por gerar-tasks após revisão das SPECs. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
