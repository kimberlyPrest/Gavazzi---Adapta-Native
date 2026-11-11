# Fase 2 — Revisão com checklist, emissão e pastas padrão

## Objetivo

Fazer a revisão dos projetos acontecer dentro da Central: cada disciplina recebe o checklist certo, o coordenador revisa item por item, o que não está conforme volta para correção com motivo e responsável, a emissão só sai depois da revisão aprovada e os indicadores de qualidade (K2 e K3) passam a ser calculados. Ao criar um projeto, a Central também cria a estrutura padrão de pastas no OneDrive, para que todo projeto nasça no mesmo padrão.

## Decisões que valem para esta fase (Kim, 11/11/2026)

- **Checklists configuráveis pela interface.** Os checklists não são pré-requisito da fase: o sistema permite criar e manter os checklists de entrada e de revisão por disciplina pela tela. Os coordenadores cadastram os checklists reais no teste final da fase (T2.22).
- **Pastas padrão no OneDrive.** Criar um projeto na Central cria a estrutura padrão de pastas no OneDrive (cliente › local/filial › projeto › disciplina › subpastas do modelo). O modelo de pastas também é configurável pela tela.
- **Revisor = coordenador do projeto.** É o que já vale no sistema desde a SPEC-1-008.

## Inclui

- modelos de checklist por disciplina e por tipo (entrada e revisão), com versões;
- checklist aplicado e congelado em cada disciplina do projeto;
- checklist de entrada com pendência de entrada (dono e prazo);
- rodadas de revisão com resultado item a item, retorno para correção e nova rodada;
- exceção técnica decidida por pessoa autorizada, com justificativa;
- registro de emissão ligado à entrega do calendário (revisão R00, R01…);
- registro de correção após a emissão, com origem e severidade;
- indicadores K2 e K3, retorno para correção e rodadas por pessoa, com exportação;
- modelo de pastas configurável e criação automática das pastas no OneDrive.

## Não inclui

Leitura automática de DWG/RVT/PDF, IA que avalie o projeto, plugins, biblioteca técnica Revit, envio de arquivos ou e-mails para clientes e qualquer apagar, mover ou renomear arquivos no OneDrive.

## Preparação da fase

- **Acesso Microsoft (T2.17):** um administrador do Microsoft 365 da Gavazzi libera o acesso de arquivos para o aplicativo que a Central já usa no login e informa a pasta raiz dos clientes no OneDrive/SharePoint. Pode ser feito a qualquer momento da fase; só a SPEC-2-006 depende disso.
- **Modelo de pastas:** foto ou lista da estrutura de pastas padrão que todo projeto deve ter (combinado na reunião de 06/10).
- Os checklists **não** precisam estar prontos antes: são cadastrados no fim (T2.22).

## SPECs

| SPEC | Resultado |
|---|---|
| SPEC-2-001 | Modelos de checklist configuráveis pela interface |
| SPEC-2-002 | Checklist aplicado ao projeto e checklist de entrada |
| SPEC-2-003 | Revisão, retorno para correção e exceção |
| SPEC-2-004 | Emissão e correções após a emissão |
| SPEC-2-005 | Indicadores de qualidade (K2 e K3) |
| SPEC-2-006 | Pastas padrão no OneDrive |

## Demonstração visível

Tomaz cria um projeto real e as pastas aparecem no OneDrive no padrão. A disciplina recebe o checklist de entrada; a pendência de entrada é resolvida. O projetista conclui e o coordenador revisa com o checklist cadastrado pelos coordenadores: dois itens não conformes voltam para correção, a segunda rodada é aprovada e a emissão R00 é registrada na entrega do calendário. Alessandro vê o K2 do projeto e o retorno para correção no painel.

## Teste do cliente

Por SPEC, não por task, como na Fase 1: seis testes, um por SPEC, quando todas as tasks da SPEC estiverem no ar. O roteiro está em `## Teste humano do cliente` de cada SPEC. No fim, os coordenadores cadastram os checklists reais (T2.22) e a demonstração final (T2.23) é o aceite da fase.

## Critérios de aceite

- **CA-2-01:** checklist de entrada e de revisão pode ser criado, editado e publicado pela interface, por disciplina, sem mexer em código.
- **CA-2-02:** editar um checklist publicado cria uma nova versão; projetos que já usam a versão anterior não mudam.
- **CA-2-03:** cada disciplina do projeto recebe a versão vigente do checklist, que fica congelada para aquela disciplina.
- **CA-2-04:** item de entrada faltante gera pendência com dono e prazo; item crítico pendente impede o avanço para "Pronto".
- **CA-2-05:** "não se aplica" exige justificativa.
- **CA-2-06:** revisão reprovada devolve para "Em correção" com itens, motivo e responsável; a nova rodada preserva a anterior.
- **CA-2-07:** exceção técnica só é aceita por coordenador/administrador, com justificativa e registro de quem decidiu.
- **CA-2-08:** emissão só é registrada com revisão aprovada e fica ligada à entrega e ao número da revisão.
- **CA-2-09:** correção após a emissão é registrada com origem, severidade e validade, e cria atividade de correção.
- **CA-2-10:** K2 e K3 são calculados pelas fórmulas do escopo, batem com a exportação e aparecem como inconclusivos quando a amostra é pequena.
- **CA-2-11:** criar projeto cria a estrutura de pastas do modelo no OneDrive e grava o link no projeto, sem duplicar pastas existentes.
- **CA-2-12:** a Central nunca apaga, move ou renomeia nada no OneDrive; falha de criação aparece na caixa de falhas e pode ser reprocessada.

## Pendências herdadas da Fase 1

Não bloqueiam as tasks desta fase.

| Pendência | Quem | Observação |
|---|---|---|
| Testes do cliente por SPEC da Fase 1 ainda não registrados | Tomaz | Registrar no changelog os testes já feitos com a equipe e os ajustes pedidos |
| T1.39 — demonstração com o projeto piloto | Tomaz + Kim | Pode ser feita junto com a demonstração da Fase 2 |
| T1.40 — decisão sobre o baseline | Kim + Tomaz | A decidir com a Kim |

## Tasks

| ID | Task | Dono | SPEC | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|---|
| T2.01 | Implementar modelos de checklist por disciplina e tipo (entrada/revisão), com itens, severidade, rascunho → publicado e versões imutáveis | Executor (Maestro) | SPEC-2-001 | CA-2-001-01..05 | TDD GREEN da SPEC-2-001 (modelo e versões) | Suíte passando + captura do editor | — | Planejada |
| T2.02 | Implementar duplicar modelo, colar itens (um por linha) e modelos de exemplo marcados como "exemplo" | Executor (Maestro) | SPEC-2-001 | CA-2-001-06, CA-2-001-07 | TDD GREEN da SPEC-2-001 (cópia e colagem) | Captura do modelo duplicado e dos itens colados | T2.01 concluída | Planejada |
| T2.03 | Teste humano da SPEC-2-001 | Tomaz + coordenador | SPEC-2-001 | Checklist de execução da SPEC-2-001 | Roteiro do teste do cliente | Checklist assinado com capturas | T2.02 concluída | Planejada |
| T2.04 | Aplicar e congelar a versão vigente do checklist em cada disciplina do projeto, na etapa configurada no Fluxo | Executor (Maestro) | SPEC-2-002 | CA-2-002-01..03 | TDD GREEN da SPEC-2-002 (aplicação e congelamento) | Teste da versão congelada após nova publicação | T2.03 concluída | Planejada |
| T2.05 | Implementar marcação por item (conforme / não conforme / não se aplica com justificativa) e pendência de entrada que segura o avanço para "Pronto" | Executor (Maestro) | SPEC-2-002 | CA-2-002-04..07 | TDD GREEN da SPEC-2-002 (entrada e avanço) | Teste de avanço negado + captura da pendência | T2.04 concluída | Planejada |
| T2.06 | Teste humano da SPEC-2-002 | Coordenador + projetista | SPEC-2-002 | Checklist de execução da SPEC-2-002 | Roteiro do teste do cliente | Checklist assinado com capturas | T2.05 concluída | Planejada |
| T2.07 | Implementar rodada de revisão pelo coordenador do projeto com resultado aprovado/reprovado e retorno para "Em correção" | Executor (Maestro) | SPEC-2-003 | CA-2-003-01..03 | TDD GREEN da SPEC-2-003 (rodada e retorno) | Suíte passando + histórico da rodada | T2.06 concluída | Planejada |
| T2.08 | Implementar correção pelo projetista e nova rodada preservando as anteriores | Executor (Maestro) | SPEC-2-003 | CA-2-003-04, CA-2-003-05 | TDD GREEN da SPEC-2-003 (nova rodada) | Histórico com duas rodadas | T2.07 concluída | Planejada |
| T2.09 | Implementar exceção técnica (coordenador/administrador, justificativa, quem decidiu) | Executor (Maestro) | SPEC-2-003 | CA-2-003-06, CA-2-003-07 | TDD RED/GREEN da SPEC-2-003 (exceção sem permissão) | Teste de exceção negada + registro da aceita | T2.07 concluída | Planejada |
| T2.10 | Teste humano da SPEC-2-003 | Coordenador + projetista | SPEC-2-003 | Checklist de execução da SPEC-2-003 | Roteiro do teste do cliente | Checklist assinado com capturas | T2.09 concluída | Planejada |
| T2.11 | Implementar registro de emissão ligado à entrega do calendário (número da revisão, data, destinatário, responsável), só com revisão aprovada | Executor (Maestro) | SPEC-2-004 | CA-2-004-01..03 | TDD GREEN da SPEC-2-004 (emissão) | Teste de emissão negada sem aprovação + captura | T2.10 concluída | Planejada |
| T2.12 | Implementar correção após emissão (origem, severidade, válida/inválida, quem decidiu) com atividade de correção na fila | Executor (Maestro) | SPEC-2-004 | CA-2-004-04..06 | TDD GREEN da SPEC-2-004 (correção pós-emissão) | Captura da correção + atividade criada | T2.11 concluída | Planejada |
| T2.13 | Teste humano da SPEC-2-004 | Coordenador | SPEC-2-004 | Checklist de execução da SPEC-2-004 | Roteiro do teste do cliente | Checklist assinado com capturas | T2.12 concluída | Planejada |
| T2.14 | Implementar K2 (1ª rodada) por projeto, disciplina, pessoa e período, com drill-down | Executor (Maestro) | SPEC-2-005 | CA-2-005-01, CA-2-005-02, CA-2-005-05 | TDD GREEN da SPEC-2-005 (fórmula K2) | Teste com fixture de resultado conhecido | T2.13 concluída | Planejada |
| T2.15 | Implementar K3, retorno para correção e rodadas por pessoa, marcação de inconclusivo e exportação CSV | Executor (Maestro) | SPEC-2-005 | CA-2-005-03, CA-2-005-04, CA-2-005-06 | TDD GREEN da SPEC-2-005 (K3 e CSV) | CSV conferindo com o painel | T2.14 concluída | Planejada |
| T2.16 | Teste humano da SPEC-2-005 | Alessandro + Tomaz | SPEC-2-005 | Checklist de execução da SPEC-2-005 | Roteiro do teste do cliente | Checklist assinado com capturas | T2.15 concluída | Planejada |
| T2.17 | Liberar o acesso de arquivos do Microsoft 365 para o aplicativo da Central e informar a pasta raiz dos clientes | Tomaz + administrador Microsoft da Gavazzi | SPEC-2-006 | Pré-condição da SPEC-2-006 | Acesso que só o cliente tem | Confirmação do acesso + caminho da pasta raiz (sem segredo em mensagem) | — | Planejada |
| T2.18 | Implementar modelo de pastas configurável pela tela, com variáveis (cliente, local, projeto, disciplina) e versões | Executor (Maestro) | SPEC-2-006 | CA-2-006-01, CA-2-006-02 | TDD GREEN da SPEC-2-006 (modelo de pastas) | Captura do editor + prévia da árvore | T2.16 concluída | Planejada |
| T2.19 | Criar as pastas no OneDrive ao criar o projeto e ao incluir disciplina, de forma idempotente, gravando o link no projeto | Executor (Maestro) | SPEC-2-006 | CA-2-006-03..06 | TDD GREEN da SPEC-2-006 (criação idempotente) | Pastas criadas no OneDrive + link no projeto | T2.17 e T2.18 concluídas | Planejada |
| T2.20 | Registrar falha de criação na caixa de falhas com reprocessamento e criar pastas para projetos já existentes (simular antes, depois aplicar) | Executor (Maestro) | SPEC-2-006 | CA-2-006-07, CA-2-006-08 | TDD RED/GREEN da SPEC-2-006 (falha e lote) | Captura da falha + relatório da simulação | T2.19 concluída | Planejada |
| T2.21 | Teste humano da SPEC-2-006 | Tomaz | SPEC-2-006 | Checklist de execução da SPEC-2-006 | Roteiro do teste do cliente | Checklist assinado com capturas do OneDrive | T2.20 concluída | Planejada |
| T2.22 | Cadastrar os checklists reais de entrada e de revisão pela interface, pelo menos para as disciplinas do projeto da demonstração | Coordenadores (Tomaz organiza) | SPEC-2-001 | CA-2-01 | Teste final de configuração | Checklists publicados (versão 1) por disciplina | T2.21 concluída | Planejada |
| T2.23 | Demonstração final da Fase 2 com projeto real | Tomaz + Kim | Fase 2 | Demonstração visível | Aceite da fase | Vídeo da demonstração + evidências dos CAs | T2.22 concluída | Planejada |

## Saída da fase

Fase encerrada após a demonstração final (T2.23), os checklists reais publicados e a aprovação da Kim. Sem amostra suficiente, K2 e K3 aparecem como inconclusivos; isso não bloqueia o encerramento, mas não vira resultado.

## Emendas

| Data | Origem do sinal | Seção | Resumo |
|---|---|---|---|
