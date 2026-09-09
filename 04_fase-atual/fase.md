# Fase 1 — Central Operacional e Baseline

## Objetivo

Entregar o sistema aprovado na reunião de 02/09: uma visão centralizada dos projetos, etapas, responsáveis, prioridades, filas e handoffs, operando pelo menos um projeto real e coletando os dados necessários para medir a operação.

## Inclui

- autenticação e papéis mínimos;
- cadastro de cliente, projeto, tipologia, disciplinas, prazo e responsáveis;
- etapas configuráveis por fluxo;
- Kanban/pipe e fila individual;
- prioridade conforme política homologada;
- bloqueio com motivo, responsável e prazo;
- handoff que cria atividade para o próximo responsável;
- histórico de transições;
- apontamento simples de touch time;
- painel de projetos por etapa, atraso, bloqueio e responsável;
- protocolo de baseline definido com o cliente e coleta “antes” em modo sombra, antes da ativação do novo fluxo.

## Não inclui

Checklist técnico detalhado, biblioteca de padrões, plugins, leitura de DWG/RVT, geração de tabelas ou validação automática.

## Preparação da fase

- confirmar a identidade documental durante o cadastro inicial;
- escolher o projeto e a tipologia piloto;
- definir protocolo de baseline com amostra, relógio, exclusões e período em modo sombra;
- configurar fluxo, etapas, alçadas, prioridade e SLA com Tomaz e coordenadores;
- definir papéis, conta corporativa e política de credenciais.

## Demonstração visível

Tomaz cadastra um projeto real, distribui disciplinas, um projetista recebe a tarefa na fila, registra bloqueio/hora, conclui a etapa e o próximo responsável recebe o handoff. Alessandro visualiza situação, atraso, responsável e tempo acumulado.

## Critérios de aceite

- **CA-1-01:** usuário sem permissão não acessa projeto restrito.
- **CA-1-02:** projeto é criado com campos mínimos e aparece no Kanban.
- **CA-1-03:** transição válida cria histórico com usuário e horário.
- **CA-1-04:** handoff cria tarefa na fila do próximo responsável.
- **CA-1-05:** bloqueio não é salvo sem motivo, dono e revisão/prazo.
- **CA-1-06:** touch time pode ser registrado por etapa sem recadastro técnico.
- **CA-1-07:** painel exibe projetos por etapa, atraso, bloqueio e responsável.
- **CA-1-08:** pelo menos um projeto piloto percorre o fluxo homologado da Entrada pendente até Aprovado em ambiente de validação.
- **CA-1-09:** baseline “antes” é coletado em modo sombra, identificado separadamente e é exportável/reproduzível.
- **CA-1-10:** trilha de auditoria registra mudança de prioridade e responsável.
- **CA-1-11:** falha de handoff/notificação fica visível, pode ser reprocessada sem duplicar tarefa e não perde histórico.
- **CA-1-12:** transições concorrentes não sobrescrevem silenciosamente estado ou responsável.
- **CA-1-13:** alteração de configuração pode ser revertida com histórico.
- **CA-1-14:** conta revogada perde acesso; política de credenciais não grava segredo em logs/documentos.
- **CA-1-15:** retenção, backup e restauração dos dados operacionais têm teste documentado.
- **CA-1-16:** completude de apontamentos e uso por papel é mensurada; o limiar padrão para leitura conclusiva é 80% de adoção e 80% de completude; abaixo disso, a medição é inconclusiva.

## Checklist manual

- [ ] Entrar como Tomaz, coordenador e projetista.
- [ ] Criar projeto piloto e disciplinas.
- [ ] Validar filas e handoffs.
- [ ] Testar bloqueio e retorno.
- [ ] Conferir histórico e painel.
- [ ] Exportar dados do baseline.

## Saída da fase

Fase encerrada somente após demonstração, evidências dos CAs e aprovação humana. Dados insuficientes não impedem o sistema, mas impedem declarar baseline conclusivo.


## Tasks vinculadas

Serão geradas por `gerar-tasks` após a aprovação das SPECs.
