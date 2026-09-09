# Escopo Definitivo — Central de Gestão e Padronização da Produção Técnica

**Estado:** aprovado pela Kim para publicação e continuidade documental.  
**Data:** 2026-09-09.

## 1. Resumo executivo

A PAG/Gavazzi começará pelo sistema aprovado na reunião de 02/09: uma central para gerir projetos, etapas, responsáveis, prioridades, handoffs, revisão e emissão. Essa fundação também cria o instrumento de medição que hoje não existe. A padronização e as automações técnicas serão adicionadas de forma seletiva e Revit-first, sempre após prova de viabilidade e sem substituir decisão de engenharia.

## 2. Inclui

### Operação e gestão
- cadastro de projeto, cliente, tipologia, disciplinas e documentos de entrada;
- etapas configuráveis e critérios de avanço;
- Kanban/pipe, filas individuais, prioridades, prazos e bloqueios;
- handoffs entre disciplinas com notificação e histórico;
- retorno para correção com motivo;
- visão executiva e operacional.

### Qualidade e padronização
- checklist de entrada e de primeira revisão;
- biblioteca de padrões por contexto;
- regras versionadas com fonte e abrangência;
- exceções com decisão humana;
- controle de revisão e emissão.

### Medição
- touch time e tempo de ciclo por etapa;
- espera e atraso por responsabilidade;
- primeira revisão, retornos e correções pós-emissão;
- cálculo reproduzível dos três KPIs.

### Automação técnica condicionada
- PoC Revit em uma tarefa repetitiva escolhida pelo cliente;
- automações Revit aprovadas pelo go/no-go;
- IA assistiva para localizar padrões/resumir pendências/sugerir classificação, somente com fonte e confirmação humana;
- fallback que ataca touch time por padronização, templates, extração não invasiva ou eliminação de handoffs — não apenas checklist;
- CAD legado somente se baixo custo, útil e homologado.

## 3. Não inclui

- geração integral de projeto por IA;
- responsabilidade, decisão ou aprovação técnica automatizada;
- migração completa para BIM;
- pacote amplo de plugins CAD;
- substituição das ferramentas de autoria técnica;
- ERP, financeiro, contratos, compras ou RH;
- aquisição/regularização de licenças;
- regras técnicas inferidas sem homologação;
- automação que imponha dupla digitação;
- envio externo irreversível sem aprovação.

## 4. Papéis

| Papel | Responsabilidade |
|---|---|
| Alessandro | patrocínio, prioridade executiva e aprovação de decisões de negócio |
| Tomaz | dono operacional e ponto focal; organização das validações |
| Coordenadores | homologar fluxo, checklist, regras e disciplina |
| Especialista técnico (Felipe) | inventariar ambiente, apoiar PoC Revit e validar reversão técnica |
| Projetistas | operar fila, registrar bloqueios/tempo e executar correções |
| Revisor/RT | revisar, decidir exceções e aprovar emissão |
| Kim | escopo, revisão técnica/segurança e liberação de fases |
| CSM/cliente | validação dos critérios de aceite e decisões operacionais |

## 5. Sequência em cinco fases

1. **Fase 1 — Central operacional e baseline:** fluxo visível operando um projeto real; coleta de tempos e bloqueios.
2. **Fase 2 — Entradas, revisão e contrato de qualidade:** checklists, correções, regras e K2/K3 instrumentados.
3. **Fase 3 — Biblioteca Revit-first e prova técnica:** padrões contextualizados e PoC de automação.
4. **Fase 4 — Automação técnica seletiva:** uma ou mais automações aprovadas, sem dupla digitação.
5. **Fase 5 — Emissão controlada, adoção e medição:** trilha completa, operação estabilizada e comparação K1–K3.

## 6. Critérios de sucesso

- **K1:** redução de 50% no touch time de elaboração+revisão do projeto piloto, referência declarada 10h→5h, sujeita ao baseline coletado em modo sombra.
- **K2:** ≥95% dos itens aplicáveis conformes na primeira revisão.
- **K3:** redução ≥50% nas correções válidas após primeira emissão.

A ausência de amostra comparável torna o KPI inconclusivo; não será convertida em sucesso por percepção.

## 7. Demonstração visível por fase

| Fase | Demonstração |
|---|---|
| F1 | projeto real percorre etapas, filas e handoffs, com histórico e tempos |
| F2 | revisão real usa checklist congelado e retorna correção rastreável |
| F3 | padrão é localizado por contexto e a PoC Revit executa/rejeita com evidência |
| F4 | automação aprovada reduz uma tarefa medida sem recadastro duplicado |
| F5 | emissão é auditável e dashboard compara baseline e pós-implantação |

## 8. Preparação e dependências por fase

- F1: confirmar identidade, piloto, protocolo de baseline, fluxo, papéis e segurança; realizar o primeiro período em modo sombra antes de ativar o novo fluxo.
- F2: receber o mapeamento de revisão/checklists e garantir disponibilidade dos coordenadores.
- F3: inventariar o parque de software e preparar ambiente Revit de teste.
- F4: seguir a decisão documentada da PoC; se reprovada, usar fallback assistido.
- F5: confirmar adoção/completude dos registros, amostra pós-implantação suficiente e operação ativa.

### Cadência
F1 semanas 1–3; F2 4–6; F3 7–9; F4 10–13; F5 14–16. Dependência não disponível reprograma a atividade afetada; não comprime revisão, segurança ou medição.

## 9. Contornos de risco

- O sistema de gestão não será apresentado como responsável isolado por K1–K3.
- Nenhuma regra técnica será universal sem escopo de aplicação.
- Nenhum plugin será prometido antes de PoC.
- Nenhuma automação de desenho será aceita se aumentar touch time total.
- A liberação de cada fase depende de demonstração e aprovação humana.

## 10. Critério de aceite geral

O escopo é aceito quando Kim e CSM/cliente validarem o objetivo, os fora de escopo, as definições operacionais dos KPIs, a sequência das cinco fases e os papéis. A publicação documental foi autorizada pela Kim em 09/09/2026. SPECs, tasks e implementação serão tratadas separadamente.
