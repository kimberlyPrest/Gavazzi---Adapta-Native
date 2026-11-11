# SPEC-2-006 — Pastas padrão no OneDrive

**Fase:** 2  
**Status:** planejada  
**Dono:** Tomaz  
**Origem no escopo:** reunião de 06/10/2026 (estrutura de pastas padrão por cliente, filial, projeto e disciplina); decisão da Kim de 11/11/2026; RN-12 (sem dupla digitação)  
**Degrau da solução:** integração mínima — o mesmo aplicativo Microsoft que a Central já usa no login, com permissão de arquivos; só cria pastas.

## Resultado observável

Ao criar um projeto na Central, a estrutura padrão de pastas aparece no OneDrive da Gavazzi, no lugar certo e com os nomes certos. O link da pasta fica no projeto. Incluir uma disciplina depois cria só a pasta dela.

## Limites e dependências

- **Inclui:** modelo de pastas configurável pela tela, com variáveis {cliente}, {local}, {projeto} e {disciplina} e um bloco de subpastas repetido por disciplina; versões do modelo; prévia da árvore antes de salvar; criação das pastas ao criar projeto e ao incluir disciplina; reaproveitar pasta que já existe com o mesmo nome; link da pasta do projeto gravado no projeto; nomes ajustados aos caracteres que o OneDrive não aceita; falha na caixa de falhas (SPEC-1-005) com reprocessamento; criar pastas para projetos já existentes, com simulação antes de aplicar.
- **Fora de escopo:** apagar, mover ou renomear qualquer item no OneDrive; enviar ou copiar arquivos; ler arquivos; sincronizar mudanças feitas direto no OneDrive.
- **Entradas e pré-condições:** acesso de arquivos liberado por um administrador do Microsoft 365 da Gavazzi e pasta raiz informada (T2.17); modelo de pastas cadastrado.
- **Saídas/artefatos:** pastas no OneDrive, link no projeto e registro de cada criação.
- **Dependências e responsáveis:** Tomaz e o administrador Microsoft da Gavazzi (T2.17). O segredo do aplicativo fica só no ambiente do Skip, nunca em código, documento, prompt ou log.
- **Risco e plano B:** sem acesso, o projeto é criado normalmente e a criação de pastas fica na caixa de falhas até o acesso ser liberado.
- **Rollback ou reversão:** desligar a criação automática na configuração; as pastas já criadas ficam como estão.

## Fluxo e regras

1. Admin/diretor cadastra o modelo em **Administração › Pastas**, por exemplo: `{cliente}/{local}/{projeto}/` e, por disciplina, `{disciplina}/Recebidos`, `{disciplina}/Revisões`, `{disciplina}/PDF`.
2. Tomaz cria o projeto na Central.
3. O sistema monta o caminho a partir da pasta raiz, cria o que falta, reaproveita o que existe e grava o link no projeto.
4. Ao incluir uma disciplina, cria só o bloco dela.
5. Se der erro, o projeto continua criado e a falha aparece na caixa de falhas.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | projeto novo com 3 disciplinas | árvore completa criada; link no projeto | — |
| Limite | pasta do cliente já existe | reaproveitada; nada duplicado | — |
| Falha | acesso expirado ou OneDrive fora do ar | projeto criado; falha visível | reprocessar pela caixa de falhas |

## Checklist de execução

- [ ] Cadastrar o modelo e conferir a prévia.
- [ ] Criar um projeto e abrir o link da pasta.
- [ ] Criar outro projeto do mesmo cliente e conferir que a pasta do cliente não duplicou.
- [ ] Incluir uma disciplina e conferir a pasta nova.
- [ ] Simular a criação para projetos existentes antes de aplicar.

## Critérios de aceite

- [ ] **CA-2-006-01:** Admin/diretor cadastra e edita o modelo de pastas pela tela, com prévia da árvore; cada publicação gera uma versão.
- [ ] **CA-2-006-02:** As variáveis {cliente}, {local}, {projeto} e {disciplina} são preenchidas com os dados do projeto; caracteres não aceitos pelo OneDrive são substituídos e campo vazio é omitido do caminho.
- [ ] **CA-2-006-03:** Criar projeto cria a árvore do modelo a partir da pasta raiz e grava o link da pasta do projeto no projeto.
- [ ] **CA-2-006-04:** Pasta existente com o mesmo nome é reaproveitada; repetir a criação não duplica nada (idempotente).
- [ ] **CA-2-006-05:** Incluir disciplina cria só o bloco dessa disciplina.
- [ ] **CA-2-006-06:** A Central não apaga, move nem renomeia nada no OneDrive, e o segredo do aplicativo não aparece em código, resposta da API ou log.
- [ ] **CA-2-006-07:** Falha de criação não impede o cadastro do projeto, aparece na caixa de falhas com motivo e pode ser reprocessada sem duplicar.
- [ ] **CA-2-006-08:** Criação para projetos existentes mostra a simulação (o que será criado e o que já existe) antes de aplicar, e só admin/diretor aplica.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | duplicação e falha que bloqueia o cadastro | criar duas vezes; simular erro do OneDrive | duplicata ou projeto não criado antes da implementação | log RED |
| GREEN | criação, reaproveitamento e disciplina nova | rodar com cliente do OneDrive simulado e depois no ambiente real | árvore correta e link gravado | suíte + captura do OneDrive |
| REFACTOR/REGRESSÃO | reprocessamento, lote e varredura de segredo | reprocessar falha; simular lote; buscar segredo em logs | sem duplicata; simulação correta; nenhum segredo | suíte + relatório |

**Dados/fixtures:** pasta raiz de teste, modelo com 2 níveis e 3 subpastas por disciplina, cliente com caractere não aceito no nome, projeto com 3 disciplinas, pasta de cliente já existente, erro simulado do OneDrive.  
**Caminhos de erro obrigatórios:** acesso negado, OneDrive indisponível, nome inválido, pasta já existente, reprocessamento repetido.  
**Evidência exigida:** testes com OneDrive simulado, captura das pastas reais e varredura de logs sem segredo.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.17 | Liberar o acesso de arquivos do Microsoft 365 para o aplicativo da Central e informar a pasta raiz dos clientes | Tomaz + administrador Microsoft da Gavazzi | Pré-condição | Acesso que só o cliente tem | Confirmação do acesso + caminho da pasta raiz (sem segredo em mensagem) | — | Planejada |
| T2.18 | Implementar modelo de pastas configurável pela tela, com variáveis e versões | Executor (Maestro) | CA-2-006-01, CA-2-006-02 | TDD GREEN (modelo de pastas) | Captura do editor + prévia da árvore | T2.16 concluída | Planejada |
| T2.19 | Criar as pastas no OneDrive ao criar o projeto e ao incluir disciplina, de forma idempotente, gravando o link no projeto | Executor (Maestro) | CA-2-006-03..06 | TDD GREEN (criação idempotente) | Pastas criadas no OneDrive + link no projeto | T2.17 e T2.18 concluídas | Planejada |
| T2.20 | Registrar falha na caixa de falhas com reprocessamento e criar pastas para projetos existentes (simular, depois aplicar) | Executor (Maestro) | CA-2-006-07, CA-2-006-08 | TDD RED/GREEN (falha e lote) | Captura da falha + relatório da simulação | T2.19 concluída | Planejada |
| T2.21 | Teste humano da SPEC-2-006 | Tomaz | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas do OneDrive | T2.20 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.18 a T2.20 no ar. T2.21 é este teste.
- **Quem testa:** Tomaz.
- **Passos:** 1) cadastrar o modelo de pastas real e conferir a prévia; 2) criar um projeto de teste e abrir o link da pasta no OneDrive; 3) criar outro projeto do mesmo cliente e conferir que a pasta do cliente não duplicou; 4) incluir uma disciplina e conferir a pasta nova; 5) rodar a simulação para os projetos existentes e conferir a lista antes de aplicar.
- **Resultado esperado:** CA-2-006-01 a CA-2-006-05 e CA-2-006-08; o CA-2-006-06 e o CA-2-006-07 fecham pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas do OneDrive e mensagem do Tomaz registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
