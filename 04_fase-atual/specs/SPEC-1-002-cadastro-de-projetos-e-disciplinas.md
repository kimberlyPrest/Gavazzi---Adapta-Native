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

<!-- Preenchida por gerar-tasks após revisão das SPECs. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
