# SPEC-1-001 — Acesso e papéis

**Fase:** 1  
**Status:** planejada  
**Dono:** Kim + Tomaz  
**Origem no escopo:** RF-01; RNF autenticação/autorização; CA-1-01/14  
**Degrau da solução:** construção mínima — fatia vertical necessária para demonstrar valor da Central sem depender de integração externa.

## Resultado observável

Usuários entram na Central com conta própria e veem apenas projetos e ações permitidos ao seu papel.

## Limites e dependências

- **Inclui:** autenticação; recuperação de acesso por token de uso único válido por 15 minutos; sessão máxima de 8 horas; bloqueio temporário após 5 tentativas inválidas em 15 minutos; papéis administrador, coordenador, projetista, revisor e executivo; ativação, bloqueio e revogação; autorização no servidor; auditoria administrativa; prevenção de segredo em logs.
- **Fora de escopo:** SSO, login social, gestão de RH, provisionamento automático e permissões por cliente externo.
- **Entradas e pré-condições:** contas de teste por papel; senha mínima de 12 caracteres; sessão máxima de 8 horas com rotação do token de sessão; mensagens uniformes para conta inexistente ou credencial inválida.
- **Saídas/artefatos:** tela de login, sessão segura, administração de usuários e matriz de autorização aplicada.
- **Dependências e responsáveis:** Kim define o contrato; Tomaz administra usuários; cada pessoa usa conta individual.
- **Risco e plano B:** se e-mail corporativo não estiver disponível, usar conta nominal temporária, nunca conta compartilhada.
- **Rollback ou reversão:** desativar usuário e revogar sessões sem apagar histórico autoral.

## Fluxo e regras

1. Usuário autentica com credencial válida.
2. Servidor carrega papel e projetos permitidos.
3. Recuperação de acesso invalida tokens anteriores e sessões existentes após redefinição.
4. Ação é autorizada antes de ler ou escrever.
5. Administrador pode revogar acesso e sessões.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | projetista ativo | abre sua fila e projetos permitidos | — |
| Limite | usuário revogado com sessão antiga | acesso negado na próxima requisição | redirecionar ao login |
| Falha | papel tenta ação não autorizada ou token expirado | servidor responde 403/expirado e audita sem registrar segredo | nenhum dado é alterado; novo token pode ser solicitado |

## Checklist de execução

- [ ] Criar contas de teste para os cinco papéis.
- [ ] Aplicar autorização no backend, não somente na interface.
- [ ] Testar revogação de sessão.
- [ ] Anexar matriz papel×ação e evidências.

## Critérios de aceite

- [ ] **CA-1-001-01:** Projetista não acessa administração nem projeto sem vínculo.
- [ ] **CA-1-001-02:** Coordenador gerencia projetos de sua responsabilidade sem administrar usuários globais.
- [ ] **CA-1-001-03:** Revisor registra revisão, mas não altera autoria de outro usuário.
- [ ] **CA-1-001-04:** Executivo consulta painéis sem editar produção.
- [ ] **CA-1-001-05:** Revogação invalida sessões e preserva histórico.
- [ ] **CA-1-001-06:** Tentativa proibida retorna 403 sem vazar existência ou conteúdo do projeto.
- [ ] **CA-1-001-07:** Token de recuperação é de uso único, expira em 15 minutos e a redefinição invalida sessões anteriores.
- [ ] **CA-1-001-08:** Após 5 tentativas inválidas em 15 minutos, novas tentativas são bloqueadas temporariamente e auditadas.
- [ ] **CA-1-001-09:** Criação, ativação, alteração de papel e revogação são restritas ao administrador e auditadas.
- [ ] **CA-1-001-10:** Logs, erros e documentos não contêm senha, token, cookie ou segredo em texto puro.
- [ ] **CA-1-001-11:** Senha com menos de 12 caracteres é rejeitada; armazenamento nunca mantém senha em texto puro.
- [ ] **CA-1-001-12:** Login e recuperação retornam mensagem uniforme para conta existente ou inexistente.
- [ ] **CA-1-001-13:** O bloqueio por 5 tentativas dura 15 minutos ou pode ser removido por administrador, com auditoria.
- [ ] **CA-1-001-14:** Renovação de sessão rotaciona o token e o token anterior deixa de ser aceito.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | acesso indevido, token reutilizado, força bruta e segredo artificial | executar matriz de autorização, recuperação, 6 tentativas e varredura de logs antes das regras | acesso indevido/token reutilizado passa ou segredo aparece antes da entrega | log RED por cenário |
| GREEN | matriz, recuperação, senha, sessão e auditoria administrativa | executar suíte por CA-1-001-01..14 | cada CA passa com mensagem uniforme e sem segredo em logs | relatório de testes por CA |
| REFACTOR/REGRESSÃO | revogação, enumeração e regressão de UI | repetir matriz via API e interface após revogar sessão | nenhum bypass e histórico preservado | capturas + logs |

**Dados/fixtures:** 5 usuários, 2 projetos, vínculos distintos e uma conta revogada.  
**Caminhos de erro obrigatórios:** credencial inválida, sessão expirada após 8 horas, token expirado/reutilizado, bloqueio por tentativas, 401, 403, usuário revogado, segredo artificial e tentativa de enumeração.  
**Evidência exigida:** relatório de testes, capturas por papel e log de revogação.

## Tasks vinculadas

<!-- Preenchida por gerar-tasks após revisão das SPECs. -->

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
