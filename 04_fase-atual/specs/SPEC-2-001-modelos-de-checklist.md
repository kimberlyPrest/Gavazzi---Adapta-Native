# SPEC-2-001 — Modelos de checklist configuráveis pela interface

**Fase:** 2  
**Status:** planejada  
**Dono:** Coordenadores  
**Origem no escopo:** RF-07; RN-05; RN-10; CA-2-01/02; decisão da Kim de 11/11/2026 (checklists pela interface)  
**Degrau da solução:** construção mínima — cadastro na própria Central, sem planilha nem código para mudar um checklist.

## Resultado observável

Um coordenador cria, edita e publica pela tela o checklist de entrada e o de revisão de uma disciplina. Mudar um checklist publicado gera uma versão nova e não altera os projetos que já usam a anterior.

## Limites e dependências

- **Inclui:** modelo de checklist por disciplina e tipo (entrada ou revisão), opcionalmente por tipologia; itens com texto, grupo, severidade (crítico/normal) e referência opcional (norma, padrão interno, observação); estados rascunho → publicado → arquivado; versão imutável a cada publicação; duplicar modelo; colar vários itens de uma vez (um por linha); modelos de exemplo por disciplina marcados como "exemplo".
- **Fora de escopo:** aplicar o checklist ao projeto (SPEC-2-002), IA sugerindo itens, importação de Excel.
- **Entradas e pré-condições:** disciplinas cadastradas (Fase 1); usuário admin/diretor ou coordenador.
- **Saídas/artefatos:** modelos e versões publicadas, prontos para a SPEC-2-002.
- **Dependências e responsáveis:** coordenadores mantêm o conteúdo; os checklists reais entram em T2.22.
- **Risco e plano B:** os exemplos servem só para testar o fluxo e ficam marcados como "exemplo" até um coordenador publicar o checklist real.
- **Rollback ou reversão:** arquivar um modelo não apaga versões nem afeta projetos que já o usam; republicar uma versão anterior cria uma versão nova com o mesmo conteúdo.

## Fluxo e regras

1. O coordenador abre **Administração › Checklists** e cria um modelo (disciplina, tipo, tipologia opcional).
2. Inclui itens (um a um ou colando a lista) e salva como rascunho.
3. Publica: o sistema grava a versão 1, imutável.
4. Ao editar o publicado, o sistema abre um rascunho; publicar gera a versão 2. Só uma versão fica vigente por disciplina, tipo e tipologia.

| Cenário | Dado/condição | Resultado esperado | Caminho de erro/recuperação |
|---|---|---|---|
| Principal | coordenador publica modelo com 10 itens | versão 1 vigente | — |
| Limite | dois modelos vigentes para a mesma disciplina/tipo/tipologia | publicação recusada com mensagem clara | arquivar ou ajustar a tipologia de um deles |
| Falha | projetista tenta editar modelo | 403 auditado | — |

## Checklist de execução

- [ ] Criar modelo de revisão da Elétrica com 5 itens colados.
- [ ] Publicar, editar um item e publicar de novo.
- [ ] Conferir as versões 1 e 2 e que a 1 não mudou.
- [ ] Duplicar o modelo para outra disciplina.

## Critérios de aceite

- [ ] **CA-2-001-01:** Admin/diretor e coordenador criam modelo por disciplina e tipo (entrada/revisão), com tipologia opcional.
- [ ] **CA-2-001-02:** Item tem texto obrigatório, grupo, severidade (crítico/normal) e referência opcional; a ordem dos itens é editável.
- [ ] **CA-2-001-03:** Publicar grava uma versão imutável numerada com autor e horário.
- [ ] **CA-2-001-04:** Editar um publicado gera nova versão; a anterior continua consultável e inalterada.
- [ ] **CA-2-001-05:** Não existem duas versões vigentes para a mesma disciplina, tipo e tipologia; projetista e administrativo não editam modelos (403 auditado).
- [ ] **CA-2-001-06:** Duplicar modelo e colar itens (uma linha = um item, linhas vazias ignoradas) funcionam.
- [ ] **CA-2-001-07:** Modelos de exemplo aparecem marcados como "exemplo" e deixam de ser vigentes quando um real é publicado para a mesma disciplina e tipo.

## TDD da SPEC

| Etapa | Prova | Comando/ação | Resultado esperado | Evidência |
|---|---|---|---|---|
| RED | edição de versão publicada e conflito de vigência | alterar versão publicada direto; publicar dois vigentes | operação aceita antes da implementação | log RED |
| GREEN | ciclo rascunho → publicado → nova versão, duplicar e colar | rodar os cenários por papel | versões imutáveis, uma vigente, permissões respeitadas | suíte + captura |
| REFACTOR/REGRESSÃO | arquivamento e exemplos | arquivar modelo em uso; publicar real sobre exemplo | projetos intactos; exemplo deixa de ser vigente | suíte |

**Dados/fixtures:** 2 disciplinas, 1 tipologia, coordenador, projetista, modelo com 5 itens e modelo de exemplo.  
**Caminhos de erro obrigatórios:** item vazio, vigência duplicada, papel sem permissão, edição de versão publicada.  
**Evidência exigida:** testes de versão e permissão e captura do editor.

## Tasks vinculadas

| ID | Task | Dono | Critério | Recorte da prova | Evidência esperada | Pré-condições | Status |
|---|---|---|---|---|---|---|---|
| T2.01 | Implementar modelos de checklist por disciplina e tipo (entrada/revisão), com itens, severidade, rascunho → publicado e versões imutáveis | Executor (Maestro) | CA-2-001-01..05 | TDD GREEN (modelo e versões) | Suíte passando + captura do editor | — | Planejada |
| T2.02 | Implementar duplicar modelo, colar itens (um por linha) e modelos de exemplo marcados como "exemplo" | Executor (Maestro) | CA-2-001-06, CA-2-001-07 | TDD GREEN (cópia e colagem) | Captura do modelo duplicado e dos itens colados | T2.01 concluída | Planejada |
| T2.03 | Teste humano da SPEC-2-001 | Tomaz + coordenador | Checklist de execução | Roteiro abaixo | Checklist assinado com capturas | T2.02 concluída | Planejada |
| T2.22 | Cadastrar os checklists reais de entrada e de revisão pela interface (teste final da fase) | Coordenadores (Tomaz organiza) | CA-2-01 | Teste final de configuração | Checklists publicados (versão 1) | T2.21 concluída | Planejada |

## Teste humano do cliente

- **Quando:** T2.01 e T2.02 no ar. T2.03 é este teste.
- **Quem testa:** Tomaz com um coordenador.
- **Passos:** 1) criar um checklist de revisão de uma disciplina colando 5 itens; 2) publicar; 3) editar um item e publicar de novo; 4) conferir que a versão 1 continua igual; 5) entrar como projetista e conferir que não consegue editar.
- **Resultado esperado:** CA-2-001-01 a CA-2-001-06; o CA-2-001-07 fecha pela prova automática.
- **Evidência do aceite:** checklist assinado com capturas e mensagem do Tomaz registrada no changelog.

## Emendas

| Data | Origem do sinal | Micro-spec/task | Motivo |
|---|---|---|---|
