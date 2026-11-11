# Changelog

## 2026-11-11 — Fase 2 liberada
- [CONSULTORIA] · 2026-11-11 · **Fase 1 encerrada e arquivada** em `05_entregas/fase-1/`, com `phase-closure-manifest.json`. Base: sistema no ar até a versão v0.0.87 (06/11), cobrindo as SPECs 1-001 a 1-007 e a SPEC-1-008. Pendências que seguem, sem bloquear a Fase 2: testes do cliente por SPEC não registrados, demonstração T1.39 e decisão do baseline T1.40.
- [CONSULTORIA] · 2026-11-11 · **SPEC-1-008 registrada como emenda da Fase 1:** papéis Diretor e Administrativo, revisão técnica pelo coordenador do projeto, calendário de entregas, timer ligado à entrega, indicadores de entregas, importação do Planner e cadastro da equipe.
- [CONSULTORIA] · 2026-11-11 · **Fase 2 liberada:** "Revisão com checklist, emissão e pastas padrão", com 6 SPECs (2-001 a 2-006) e 23 tasks (T2.01–T2.23). Decisões da Kim: checklists configurados pela interface (os reais entram no teste final, T2.22) e pastas padrão criadas no OneDrive ao criar o projeto (SPEC-2-006). A emissão ligada à entrega entra na Fase 2 por causa do K3.
- [CONSULTORIA] · 2026-11-11 · Escopo definitivo ganha a seção `## 11. Emendas`; visão do programa, matriz de rastreabilidade, `AGENTS.md`, `README.md` e `STATUS.md` atualizados; nova `03_documentos/05-Matriz-SPECs-Fase-2.md`; manifesto passa para a fase 2. Fases 3 a 5 a decidir.

## 2026-10-30 — correção
- [CONSULTORIA] · 2026-10-30 · **Correção do roteiro de teste por SPEC.** Retirado o papel/conta de Felipe (especialista técnico de ambiente no escopo, sem conta na Central nem papel entre os cinco) e a revogação de conta de pessoa real: o teste da SPEC-1-001 passa a ser feito pelo Tomaz com a própria conta, os cinco papéis são provados pelas contas de fixture do T1.01 e a revogação usa uma conta de teste. Removido o ponto de aprovação que só a SPEC-1-001 tinha. Faixas de CA de 003, 005, 006 e 007 passam a citar só o que o roteiro demonstra, com o resto fechando pela prova automática; ordem de prioridade de 004 passa a "regra padrão vigente"; evidência de aceite alinhada ao checklist de execução já previsto nas tasks, sem trocar critério por mensagem. `AGENTS.md` ressalva as sete tasks de teste humano e nomeia as paradas reais (T1.39, T1.40); `fase.md` ganha a seção `## Emendas` no lugar do bullet solto; `STATUS.md` atualizado em 30/10. Nenhum critério, escopo, status ou TDD mudou; manifest segue intocado (já inconsistente antes, 11/27 → 13/27 após o commit anterior).
- [CONSULTORIA] · 2026-10-30 · **Teste do cliente por SPEC, não por task.** Sete SPECs da Fase 1 receberam a seção `## Teste humano do cliente` com um roteiro de 3 a 5 passos cada, quando todas as tasks da SPEC estiverem no ar, testado por quem já estava combinado (Tomaz, coordenador, projetista e Alessandro) e com o critério de aceite preservado. `AGENTS.md` e `CLAUDE.md` passam a dizer que as tasks são construídas em sequência, sem pedir autorização nem teste entre elas; `fase.md` e `STATUS.md` registram os sete testes da fase. Nenhuma task foi criada, fundida ou apagada; nenhum critério, escopo ou status mudou. Paradas que continuam: pergunta que muda implementação, acesso que só o cliente tem, a demonstração final (T1.39) e a decisão do baseline (T1.40).

## 2026-10-06
- Tasks da Fase 1 geradas (T1.01–T1.40) a partir das 7 SPECs, sincronizadas nas três projeções (fase.md, Tasks vinculadas das SPECs e matriz de rastreabilidade).
- STATUS atualizado: primeira task elegível = T1.01.

## 2026-09-09
- Escopo definitivo aprovado pela Kim e publicado.
- Pasta oficial do cliente criada.
- Fase 1 preparada para validação do fluxo operacional.
- Nenhuma implementação de código iniciada.

## 2026-09-09 — correção
- SPEC documental removida.
- Sete SPECs de produto da Fase 1 adicionadas, com TDD e critérios de aceite.
