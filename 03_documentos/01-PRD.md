# PRD — Central de Gestão e Padronização da Produção Técnica

## 1. Identificação

- **Cliente:** PAG / Gavazzi Engenharia — identidade contratual a confirmar no cadastro inicial.
- **Produto:** Central de Gestão e Padronização da Produção Técnica.
- **Ponto focal operacional:** Tomaz.
- **Patrocinador/aprovador executivo:** Alessandro.
- **Consultora técnica:** Kim.
- **Horizonte:** até 16 semanas: F1 semanas 1–3; F2 semanas 4–6; F3 semanas 7–9; F4 semanas 10–13; F5 semanas 14–16. Dependências não disponíveis podem reprogramar o cronograma; atraso de insumo do cliente reprograma a fase sem comprimir validação ou segurança.

## 2. Problema

A operação tem demanda, mas perdeu eficiência. Projetos percorrem disciplinas e revisões com informação dispersa, handoffs dependentes de comunicação manual, regras concentradas em especialistas e conferências repetitivas entre desenho, tabelas e padrões. A empresa está migrando para Revit, mas os materiais observados ainda refletem parte relevante do legado CAD/ZWCAD.

## 3. Objetivo do produto

Criar uma operação visível, rastreável e mensurável para a produção técnica e, sobre essa fundação, padronizar entradas, revisão e emissão e aplicar automações seletivas Revit-first que reduzam trabalho repetitivo sem transferir decisão de engenharia ao sistema.

## 4. Resultados de negócio

### K1 — Horas por projeto piloto
- **Meta do briefing:** reduzir 50%, referência declarada ≈10h→5h.
- **Definição operacional:** soma do touch time de elaboração e revisão até aprovação no padrão PAG; esperas são medidas separadamente.
- **Amostra:** projetos comparáveis da mesma tipologia e disciplina; tamanho mínimo definido com o cliente, recomendação inicial n≥5 antes e n≥5 depois.
- **Coleta antes:** modo sombra antes da ativação do novo fluxo operacional; o sistema apenas observa/registra o processo atual. Se não houver amostra anterior suficiente, K1 será inconclusivo e não comparado à estimativa de 10h.
- **Estado atual:** referência declarada, não baseline medido.

### K2 — Aderência ao checklist na primeira revisão
- **Meta:** ≥95%.
- **Fórmula:** itens conformes na primeira revisão ÷ itens aplicáveis verificados.
- **Regras:** itens não aplicáveis exigem justificativa; checklist e versão ficam congelados por projeto.
- **Estado atual:** checklist consolidado não entregue.

### K3 — Correções após a primeira emissão
- **Meta:** redução ≥50% contra baseline medido.
- **Fórmula:** correções válidas pós-emissão por projeto comparável, separadas por origem e severidade.
- **Estado atual:** fonte e baseline não definidos.

### Indicadores operacionais de apoio
- tempo de ciclo e touch time por etapa;
- espera por handoff e entrada externa;
- taxa de retorno para correção;
- projetos/tarefas atrasados por responsável e disciplina;
- lead time de revisão;
- adesão à atualização do sistema.

## 5. Usuários e necessidades

- **Tomaz/ponto focal:** visão geral, prioridades, bloqueios, cobrança e configuração do fluxo.
- **Coordenadores:** distribuir, revisar, aprovar exceções e acompanhar disciplina/equipe.
- **Projetistas:** fila individual, dados de entrada, checklist, prazo, pendências e retorno de revisão.
- **Revisores/engenheiros responsáveis:** checklist versionado, divergências, justificativas, aprovação e emissão.
- **Alessandro:** visão executiva de produtividade, qualidade, capacidade e gargalos.

## 6. Fluxo-alvo

1. Projeto é cadastrado com cliente, tipologia, disciplinas, prazo, prioridade e responsáveis.
2. Cada disciplina passa por triagem de entradas; falta gera pendência com dono e prazo.
3. O projeto entra na fila do responsável quando os critérios da etapa são atendidos.
4. A elaboração ocorre no Revit ou ferramenta legada; o sistema registra estado, tempo e evidências, sem exigir dupla digitação técnica.
5. Handoffs entre disciplinas criam tarefas e notificações rastreáveis.
6. A revisão usa checklist aplicável e versionado.
7. Reprovação retorna para correção com motivo, item e responsável.
8. Exceções exigem decisão humana registrada.
9. Emissão exige aprovação humana e registra revisão, data e destinatário.
10. Painéis calculam operação e KPIs conforme protocolo congelado.

### Estados mínimos
`Entrada pendente` → `Pronto` → `Em elaboração` → `Aguardando revisão` → `Em correção` → `Aprovado` → `Emitido`; `Bloqueado` é transversal e exige motivo/dono/prazo.

## 7. Requisitos funcionais

- **RF-01:** cadastro de projetos, disciplinas, responsáveis, prazos e prioridade.
- **RF-02:** etapas configuráveis por tipologia/disciplina, com critérios de entrada e saída.
- **RF-03:** filas individuais e visão por coordenador.
- **RF-04:** handoffs automáticos e pendências rastreáveis.
- **RF-05:** histórico de transições, bloqueios e responsáveis.
- **RF-06:** apontamento simples de touch time por etapa e projeto.
- **RF-07:** checklist de entrada e revisão, versionado e contextual.
- **RF-08:** retorno para correção com motivo e item do checklist.
- **RF-09:** exceção técnica com justificativa e aprovação humana.
- **RF-10:** registro de emissão/revisão/destinatário.
- **RF-11:** dashboards operacionais e K1–K3.
- **RF-12:** biblioteca de padrões por cliente, tipologia, disciplina e versão.
- **RF-13:** PoC de automação Revit com resultado reproduzível.
- **RF-14:** automação técnica seletiva somente após go/no-go.
- **RF-15:** notificações e cobranças configuráveis sem substituir a responsabilidade do usuário.
- **RF-16:** IA assistiva, condicionada a dados e padrões homologados, para localizar padrões, resumir pendências e sugerir classificação/checklist; toda sugestão exige confirmação humana e nunca cria decisão técnica.

## 8. Requisitos não funcionais

- autenticação e autorização por papel;
- segregação de projetos e informações por necessidade de acesso;
- trilha de auditoria imutável para transições, exceções e emissões;
- nenhuma credencial pessoal gravada em documento, prompt ou log;
- conta corporativa dedicada para conectores;
- exportação dos dados operacionais;
- reversibilidade de configuração e automações;
- interface responsiva para consulta e atualização rápida;
- tempos e métricas calculados de forma reproduzível;
- automação não pode aprovar decisão técnica nem emitir sem humano;
- proteção de dados e confidencialidade por projeto, com retenção, backup e revogação de acesso definidos;
- IA, quando usada, deve citar a fonte/padrão que fundamenta a sugestão e permitir rejeição.

## 9. Regras de negócio

- **RN-01:** toda tarefa tem responsável, prazo e etapa.
- **RN-02:** bloqueio exige motivo, dono da resolução e data de revisão.
- **RN-03:** avanço automático ocorre apenas quando critérios configurados forem atendidos.
- **RN-04:** prioridade segue política definida com Tomaz e coordenadores; alteração fica auditada.
- **RN-05:** checklist aplicável é congelado por projeto/revisão.
- **RN-06:** “não aplicável” exige justificativa.
- **RN-07:** reprovação cria retorno rastreável para correção.
- **RN-08:** exceção técnica exige decisão de profissional autorizado.
- **RN-09:** emissão exige revisão aprovada e registro da pessoa responsável.
- **RN-10:** regra técnica tem fonte, abrangência, versão, dono e vigência.
- **RN-11:** item extraído de Revit/CAD só pode alimentar tabela/validação se a origem for tecnicamente comprovada.
- **RN-12:** na ausência de integração provada, usar checklist assistido; não exigir recadastro técnico duplicado.
- **RN-13:** sugestão de IA não altera estado, checklist, modelo ou emissão sem confirmação humana.
- **RN-14:** baseline “antes” deve ser coletado em modo sombra; dados já produzidos sob o novo fluxo não podem compor o grupo de controle.

## 10. Fora de escopo

- IA ou automação gerando projeto integral e assumindo responsabilidade técnica;
- decisão normativa ou aprovação de engenharia pelo sistema;
- migração completa CAD→BIM/Revit;
- automação pesada em AutoCAD/ZWCAD;
- substituir Revit/CAD, ERP, financeiro ou gestão de contratos;
- regularização/aquisição de licenças;
- integrações com sistemas não inventariados;
- leitura autônoma de documentos técnicos como fonte soberana;
- comunicação externa automática com cliente/obra sem aprovação.

## 11. Premissas operacionais

Durante as fases serão confirmados: identidade documental; projeto piloto; protocolo e coleta em modo sombra; fluxo, alçadas, prioridade e SLA; revisão e checklist; parque de software; segurança; PoC Revit; adoção mínima e completude dos registros. Essas confirmações fazem parte do trabalho de cada fase e não impedem o início do programa.

## 12. Critério de conclusão do programa

O produto está operando em projetos reais, os cinco fluxos/fases foram demonstrados, K1–K3 foram calculados contra protocolo congelado e quaisquer resultados inconclusivos estão documentados sem substituir ausência de evidência por estimativa.
