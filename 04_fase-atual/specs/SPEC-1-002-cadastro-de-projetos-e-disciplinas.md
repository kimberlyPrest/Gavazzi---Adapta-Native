# SPEC-1-002 — Cadastro de projetos e disciplinas

**Fase:** 1  
**Status:** planejada  
**Dono:** Tomaz  
**Origem no escopo:** RF-01; RN-01; CA-1-02  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Tomaz cadastra um projeto técnico com cliente, tipologia, disciplinas, prazo e responsáveis e o projeto fica pronto para operar.

## Limites e dependências

- **Inclui:** clientes; projetos; disciplinas; responsáveis; prazo; prioridade inicial; links HTTPS de entrada sem fetch/preview no servidor, rejeitando localhost, loopback, link-local, IPs privados e URL com credencial embutida; status inicial; edição controlada; autorização para criar/editar clientes e projetos.
- **Fora de escopo:** gestão de contratos, financeiro, armazenamento de DWG/RVT e cadastro técnico de itens.
- **Entradas e pré-condições:** usuário autorizado e campos mínimos definidos no PRD.
- **Saídas/artefatos:** cadastro validado, detalhe 360º do projeto e disciplinas vinculadas.
- **Dependências e responsáveis:** Tomaz/coordenador cadastra; projetistas são vinculados por disciplina.
- **Risco e plano B:** se identidade comercial não estiver finalizada, aceitar nome operacional e permitir correção auditada.
- **Rollback ou reversão:** arquivar projeto ou restaurar versão anterior dos metadados sem excluir histórico.

## Fluxo e regras

1. Usuário cria ou localiza o cliente.
2. Informa dados mínimos do projeto.
3. Seleciona uma ou mais disciplinas e responsáveis.
4. Sistema valida, grava e abre o detalhe do projeto.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | campos mínimos válidos | projeto criado uma vez com disciplinas | — |
| Limite | mesmo cliente/local/tipologia | alerta de possível duplicidade | usuário confirma ou abre existente |
| Falha | prazo inválido ou sem disciplina | gravação rejeitada com campos destacados | corrigir e reenviar |

## Checklist de execução

- [ ] Criar fixture de cliente e usuários.
- [ ] Cadastrar projeto com duas disciplinas.
- [ ] Testar duplicidade e edição.
- [ ] Anexar evidência do detalhe e histórico.

## Critérios de aceite

- [ ] **CA-1-002-01:** Projeto não é criado sem cliente, nome/local, tipologia, ao menos uma disciplina, prazo e responsável.
- [ ] **CA-1-002-02:** Cadastro válido aparece no detalhe e na listagem sem duplicação.
- [ ] **CA-1-002-03:** Cada disciplina possui responsável próprio ou herda responsável explicitamente mostrado.
- [ ] **CA-1-002-04:** Possível duplicidade gera alerta antes de salvar.
- [ ] **CA-1-002-05:** Edição de prazo, prioridade ou responsável registra antes, depois, autor e horário.
- [ ] **CA-1-002-06:** Arquivamento remove o projeto das filas ativas sem apagar histórico.
- [ ] **CA-1-002-07:** Somente administrador ou coordenador autorizado cria/edita cliente e projeto; consultas não permitem enumerar clientes fora do escopo do usuário.
- [ ] **CA-1-002-08:** Link de entrada aceita somente HTTPS, não é buscado pelo servidor, rejeita localhost/loopback/link-local/IP privado/credencial embutida e herda as permissões do projeto.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | validações, autorização e links inseguros ausentes | enviar payload sem disciplina/responsável, enumerar cliente e salvar URLs inseguras | dado inválido, enumeração ou URL insegura passa antes da entrega | resultado RED por cenário |
| GREEN | cadastro vertical completo e responsável por disciplina | executar testes de criação, herança/exibição de responsável, detalhe e listagem | projeto válido aparece uma vez, responsável é explícito e inválidos falham | suíte + captura |
| REFACTOR/REGRESSÃO | duplicidade, concorrência e arquivamento | criar simultaneamente e editar/arquivar/restaurar | sem duplicação silenciosa e histórico íntegro | logs + export |

**Dados/fixtures:** 1 cliente, 2 projetos semelhantes, 5 usuários e 4 disciplinas.  
**Caminhos de erro obrigatórios:** campos vazios, data passada inválida, duplicidade, conflito de edição, projeto arquivado, enumeração de cliente e link HTTP/domínio não permitido.  
**Evidência exigida:** vídeo curto do cadastro, respostas de teste e histórico exportado.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T1.07 | Criar fixture de cliente, disciplinas e projetos semelhantes (1 cliente, 2 projetos, 4 disciplinas) | Executor (Maestro) | Fixture carrega e reflete os dados descritos na SPEC | Dados/fixtures da SPEC-1-002 | Seed executado + listagem | T1.06 concluída | Planejada |
| T1.08 | Implementar cadastro de cliente/projeto/disciplinas com campos mínimos, responsável por disciplina e detalhe 360º | Executor (Maestro) | CA-1-002-01, CA-1-002-02, CA-1-002-03 | TDD GREEN da SPEC-1-002 (cadastro vertical) | Suíte passando + captura do detalhe do projeto | T1.07 concluída | Planejada |
| T1.09 | Implementar alerta de duplicidade, edição auditada e arquivamento sem apagar histórico | Executor (Maestro) | CA-1-002-04, CA-1-002-05, CA-1-002-06 | TDD REFACTOR/REGRESSÃO da SPEC-1-002 (duplicidade e arquivamento) | Logs de edição/arquivamento + alerta de duplicidade | T1.08 concluída | Planejada |
| T1.10 | Implementar autorização de criação/edição e validação de link de entrada (somente HTTPS, sem fetch no servidor) | Executor (Maestro) | CA-1-002-07, CA-1-002-08 | TDD RED/GREEN da SPEC-1-002 (enumeração e links inseguros) | Testes de URL insegura rejeitada + 403 de enumeração | T1.08 concluída | Planejada |
| T1.11 | Teste humano da SPEC-1-002: cadastrar projeto real com duas disciplinas e validar duplicidade/edição | Tomaz | Checklist de execução da SPEC-1-002 | Vídeo curto do cadastro + histórico exportado | Checklist assinado | T1.10 concluída | Planejada |

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|