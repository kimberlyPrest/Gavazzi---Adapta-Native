# SPEC-1-000 — Preparação do fluxo operacional

## Resultado

Validar com Tomaz e coordenadores o contrato operacional necessário para configurar a Central da Fase 1, sem implementar código nesta SPEC.

## Inclui
- etapas e estados do fluxo;
- responsáveis e alçadas;
- política de prioridade;
- handoffs e tratamento de bloqueios;
- projeto/tipologia piloto;
- relógio, amostra e período em modo sombra do baseline;
- papéis de acesso e conta corporativa.

## Não inclui

Código, banco de dados, interface, plugin Revit, integração CAD/Revit, IA ou automação técnica.

## Checklist
- [ ] Etapas e estados validados.
- [ ] Responsáveis e alçadas registrados.
- [ ] Prioridade e SLAs definidos.
- [ ] Handoffs e bloqueios definidos.
- [ ] Projeto piloto escolhido.
- [ ] Protocolo de modo sombra definido.
- [ ] Papéis de acesso definidos.

## Critérios de aceite
- **CA-1-000-01:** a ata registra etapas, estados e critérios de transição sem ambiguidade.
- **CA-1-000-02:** cada etapa tem responsável e alçada de decisão.
- **CA-1-000-03:** projeto piloto e protocolo de baseline estão identificados.
- **CA-1-000-04:** nenhum item da SPEC pressupõe implementação concluída.

## TDD documental

### RED
Tentar configurar o fluxo usando apenas a reunião de 02/09; a configuração falha por ausência de etapas, alçadas, prioridade e relógio detalhados.

### GREEN
Realizar a validação com Tomaz/coordenadores e preencher a ata/checklist até todos os critérios serem binários.

### REFACTOR
Remover duplicidades, consolidar termos e verificar que o fluxo não depende de conhecimento tácito para ser configurado.

## Tasks vinculadas
- T1.0 — Validar fluxo operacional da Fase 1.
