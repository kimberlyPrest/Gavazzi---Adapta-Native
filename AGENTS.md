# PAG/Gavazzi — Projeto Adapta Native

Execute somente a fase atual e siga as SPECs e tasks publicadas. Não altere critérios de aceite, responsabilidade técnica ou escopo sem aprovação da consultora.

## Ritmo e teste do cliente
Vale desde 30/10/2026 e substitui o ritmo antigo, em que cada task pedia autorização e teste.

- Construa as tasks em sequência, uma por vez, sem pedir autorização nem teste entre elas. Cada task fecha pelas provas automáticas da SPEC (RED, GREEN, REGRESSÃO) e pelas evidências que ela já exige; as sete tasks de teste humano (T1.06, T1.11, T1.16, T1.20, T1.25, T1.31 e T1.38) fecham pelo teste do cliente da SPEC.
- O teste do cliente é por SPEC e segue `## Teste humano do cliente` de cada uma: nesta fase são sete, um por SPEC, na ordem das SPECs.
- Continuam paradas: pergunta que muda implementação, acesso que só o cliente tem, a demonstração final (T1.39) e a decisão do baseline (T1.40). Preservar segurança, integrações e dados em uso.

## Regras essenciais
- Decisões e emissão de engenharia permanecem humanas.
- Priorizar Revit; CAD é legado e só entra quando houver valor comprovado.
- Não gerar projeto integral com IA.
- Não criar dupla digitação entre o sistema e as ferramentas técnicas.
- Não gravar credenciais em arquivos, prompts ou logs.
