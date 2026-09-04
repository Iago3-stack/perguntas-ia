# Guardrails & Segurança de LLM — 2 dúvidas sobre colocar limites no modelo

## 1. Guardrails — "não é só filtrar palavras proibidas?"

**Pergunta:** *"Falam em 'guardrails' pra IA segura. Não é só criar uma lista de palavras bloqueadas e pronto? O que mais existe além do filtro?"*

**Resposta:** Lista de palavras é só a camada mais rasa — e já caiu em desuso sozinha (modelos contornam com sinônimos, contexto, codificação). Guardrails de verdade têm **várias camadas que se reforçam**: **(1) entrada** — sanitização e validação do input (prompt injection, limite de tamanho); **(2) saída** — verificação do que o modelo gerou (filtros de conteúdo, formatação, schema no JSON, detector de alucinação); **(3) política** — regras de negócio/segurança que o sistema aplica (ex: negar ação de *delete*); **(4) humano-no-loop** — casos críticos sobem para revisão humana. Frameworks como Guardrails AI, NeMo Guardrails e Llama Guard implementam isso como *validators*, que são regras executáveis sobre a resposta do modelo — não apenas strings bloqueadas.

**Por que interessa:** em produção, a diferença entre "usei LLM" e "sistema com LLM seguro" está exatamente nessas camadas. Para um QA, saber testar cada camada (injeção, formatação, alucinação, política) é o equivalente ao **teste de requisitos não-funcionais** — e é o que recrutadores querem ouvir quando perguntam "como você garante segurança em IA?".

**Exemplo meu:** no meu motor de triagem híbrido, já aplico um "guardrail" simples de saída: o `ia.py` pede **JSON estrito** ao Gemini e tem `_extrair_json` pra validar o formato antes de usar. Se o LLM devolver texto fora do schema, o fallback deixa o motor local no comando — ou seja, o guardrail (validação de schema) impede que resposta malformada quebre a aplicação. Evoluindo, o próximo passo seria um validator que recusa severidade "alta" para relatos sem evidência técnica — regra de política, não de palavra.

---

## 2. Segurança — "se o agente tem ferramentas, como eu impeço ele de fazer besteira?"

**Pergunta:** *"O agente pode executar ações no sistema (pagar, deletar, enviar). Como eu garanto que ele não faz uma ação perigosa? Filtro de prompt resolve?"*

**Resposta:** Não — **segurança de ações não se resolve em prompt** (o modelo pode ser injetado ou enganado). A regra de ouro: **a decisão do LLM nunca é autorização final**. Guardrails de ação funcionam com: **(1) permitir por padrão** — o agente só executa ações na allowlist (nada "de fora" é permitido); **(2) validação estrutural** — antes de chamar a ferramenta, o sistema valida argumentos contra regras (valores, limites, destinos) e **recusa o que não encaixa**; **(3) separação de privilégios** — o runtime executa com credencial mínima, e ações irreversíveis exigem confirmação humana; **(4) trilha/auditoria** — para saber quem (usuario/IA) fez o quê e quando. Prompt engineering melhora comportamento; **guardrails garantem comportamento**.

**Por que interessa:** é a diferença entre "agente de demonstração" e "agente que pode ir pra produção". Em entrevistas de agemaker/IA-Arq, a pergunta chave é: "onde está o check de segurança?" — e a resposta correta é "no código, com validação estrutural e allowlist", nunca "no prompt". Para QA, isso é escrever **casos de teste adversarial**: injetar prompt malicioso, forçar ação fora da allowlist, testar recusa.

**Exemplo meu (MCP server de QA):** se o agente "Zeca" tiver permissão de criar issue no Jira, eu não deixo ele simplesmente chamar `criar_issue`. O guardrail valida antes: relato não-vazio, prioridade ∈ {baixa, media, alta, critica}, e o Jira tem credencial de **só-escrita** (sem deletar/alterar). Qualquer chamada fora disso é **recusada e logada** antes de chegar na API. O LLM propõe, o guardrail autoriza, o Jira executa — três camadas separadas.

---

*(Referência cruzada: conecta com `2026-09-04-function-calling-tools.md` — tool_choice e validação de argumentos são guardrails de ação — e com `2026-09-04-evals-llm-qa.md`, pois medir recusas e acertos de política também é eval.)*