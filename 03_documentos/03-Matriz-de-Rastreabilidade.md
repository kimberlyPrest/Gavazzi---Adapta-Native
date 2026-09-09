# Matriz de Rastreabilidade — PAG / Gavazzi

## Fontes e decisões

| Origem | Evidência/decisão | Requisito/contorno | Fase | Prova |
|---|---|---|---|---|
| Reunião 02/09 04:00–11:16 | gestão do processo aprovada | RF-01–06; pipe, filas, handoffs | F1 | CA-1-02–10 |
| Reunião 02/09 03:42–04:00 | Tomaz ponto focal | governança/RACI | F1/F5 | CA-1-08; CA-5-11 |
| Briefing K1 | 10h→5h | protocolo/touch time | F1/F4/F5 | CA-1-06/09; CA-4-08; CA-5-06/10 |
| Briefing K2 | ≥95% 1ª revisão | checklist congelado/aplicável | F2/F5 | CA-2-01–10; CA-5-07/10 |
| Briefing K3 | −50% correções pós-emissão | fonte, severidade, baseline | F2/F5 | CA-2-07/10; CA-5-08/10 |
| Reunião 08:46–10:52 | Revit-first; CAD 30–40% e caindo | inventário, PoC e CAD legado | F3/F4 | CA-3-03–10; CA-4-01–10 |
| Reunião 09:52–10:52 | não gerar projeto integral | fora de escopo; humano decide | todas | CA-3-08; CA-4-04/06; CA-5-01 |
| Vídeo 01 03:14–06:11 | limpeza manual | candidata a automação, não promessa | F3/F4 | PoC + CA-4-08 |
| Vídeo 02 03:27/03:40 | interferência/isométrico manual | hipótese Revit; decisão humana | F3/F4 | CA-3-07–09 |
| Vídeo 03 03:09–04:35 | tabela×desenho manual | evitar dupla digitação | F3/F4 | CA-3-07; CA-4-07/08 |
| Vídeo 04 00:20/00:38/03:56 | cálculo/tabela desconectados | confirmação de origem/integração | F3/F4 | CA-3-05/07/09 |
| Vídeo 05 | dependências e emissão | handoff, exceção, emissão humana | F1/F2/F5 | CA-1-04/05; CA-2-03/04; CA-5-01–03 |
| AC-001 | escopo-base divergente | substituição pela Central | F1 | CA-1-08 |
| AC-002 | Kanban não move sozinho KPIs | separar fundação e técnica | F1–F5 | demonstrações por fase |
| AC-003 | baseline insuficiente | protocolo e modo sombra | F1/F2/F5 | exportação reproduzível |
| AC-004 | CAD contraria estratégia | Revit-first | F3/F4 | inventário e go/no-go |
| AC-005 | Revit não provado | PoC obrigatória | F3 | CA-3-04–10 |
| AC-006 | risco de dupla digitação | RN-11/RN-12 | F3/F4 | CA-4-07 |
| AC-007 | revisão não mapeada | checklist e revisão reais | F2 | CA-2-01–10 |
| AC-008 | regras variáveis | fonte/abrangência/versão | F2/F3 | CA-2-02/09; CA-3-01/02 |
| AC-009 | alçadas/prioridade/SLA | configuração e papéis | F1/F2 | CA-1-03–05/10 |
| AC-010 | segurança/RT | acesso/auditoria/humano | todas | CA-1-01/10; CA-5-01–04 |
| AC-011 | adoção/governança | RACI e rotina semanal | F1/F5 | CA-1-08; CA-5-11 |
| AC-012 | software desconhecido | inventário | F3 | CA-3-03 |
| AC-013 | identidade inconsistente | confirmação no cadastro inicial | F1 | registro cadastral |

## Cobertura dos requisitos funcionais

| Requisito | Fase | Critérios principais |
|---|---|---|
| RF-01 Cadastro | F1 | CA-1-02 |
| RF-02 Etapas configuráveis | F1 | CA-1-03/08 |
| RF-03 Filas | F1 | CA-1-04/07 |
| RF-04 Handoffs | F1 | CA-1-04 |
| RF-05 Histórico | F1 | CA-1-03/10 |
| RF-06 Touch time | F1/F5 | CA-1-06/09/16; CA-5-06/13 |
| RF-07 Checklists | F2 | CA-2-01–03/08/09 |
| RF-08 Correção | F2 | CA-2-04/05 |
| RF-09 Exceções | F2/F5 | CA-2-03; CA-5-03 |
| RF-10 Emissão | F5 | CA-5-01–03 |
| RF-11 Dashboards | F1/F2/F5 | CA-1-07; CA-2-06/10; CA-5-05–10 |
| RF-12 Biblioteca | F3 | CA-3-01/02 |
| RF-13 PoC Revit | F3 | CA-3-04–10 |
| RF-14 Automação seletiva | F4 | CA-4-01–10 |
| RF-15 Notificações | F1/F5 | CA-1-04/11; CA-5-04 |
| RF-16 IA assistiva | F3/F4/F5 | CA-3-11/12; CA-4-12; CA-5-14 |

## Preparação e responsáveis

| Preparação | Evidência esperada | Responsável principal | Momento |
|---|---|---|---|
| Identidade | razão social/nome comercial confirmados | Alessandro/Kim | cadastro inicial |
| Piloto | tipologia, disciplinas e projetos comparáveis | Alessandro/Tomaz | F1 |
| Baseline | protocolo, relógio, amostra, exclusões e modo sombra | Kim + cliente | F1 e medição |
| Fluxo | etapas, alçadas, prioridade e SLA | Tomaz/coordenadores | F1 |
| Revisão | vídeo, checklist e amostra de erros | coordenadores | F2 |
| Software | versões, licenças e ambientes | Felipe + Tomaz | F3 |
| Segurança | papéis, conta e credenciais | cliente/Kim | F1 |
| Revit | PoC e decisão go/no-go | Felipe + coordenadores + Kim | F3/F4 |
| Adoção | limiar e completude por papel | Tomaz + cliente | F5 |

## Verificação final de rastreabilidade

- 13 achados cobertos por requisito, premissa, fora de escopo ou fase.
- 6 decisões explícitas cobertas.
- 16 requisitos funcionais com fase e critério.
- Exatamente cinco fases.
- Nenhuma SPEC ou task gerada antes dos checks humanos.
