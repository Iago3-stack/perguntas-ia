# LLMOps & Observabilidade — 2 dúvidas sobre monitorar sistemas com LLM

## 1. Observabilidade de LLM — "não é só log com nome novo?"

**Pergunta:** *"Falam em 'observabilidade de LLM', 'tracing', 'LLMOps'... Mas monitorar API não é a mesma coisa de ver log de erro? O que muda quando o sistema usa LLM?"*

**Resposta:** O conceito vem de MLOps/Microserviços, mas o **objeto muda**: em LLM, os fatores de falha são **input-dependentes e probabilísticos** — o mesmo código pode funcionar bem com um prompt e falhar com outro. Observabilidade de LLM é **rastrear o que o modelo fez e por quê**: qual prompt foi enviado, quais ferramentas foram chamadas (tracing), quantos tokens (custo/latência), qual modelo respondeu (fallback!), e o **resultado de cada eval** (se a resposta passou nos validators). Ferramentas como LangSmith, Langfuse, Phoenix e Arize fazem isso com: **traces** (o fluxo completo de uma chamada), **spans** (cada step: prompt → LLM → tool → resposta), e **dashboards de custo/latência/alucinação**. Não é "log bonito" — é a **base pra debugar e melhorar systems de LLM**.

**Por que interessa:** quando algo dá errado num sistema com LLM, "o log de erro" quase nunca explica *por quê* (o erro foi o prompt? o modelo deu resposta ruim? um tool retornou dados errados?). Quem sabe ler um trace interpreta a cadeia inteira — e isso separa quem debuga às cegas de quem debuga com dados. Para QA de LLM, é a ferramenta que transforma "de vez em quando funciona" em "medimos as falhas e atacamos a causa".

**Exemplo meu:** no meu triagem híbrido, o fallback entre modelos é exatamente o tipo de coisa que precisa de observabilidade. Eu queria um trace mostrando: `relato → motor local (score -5.7) → Gemini 3.5 (severidade alta) → reconcile (CRÍTICA) → gerou Gherkin`, com tokens e latência de cada modelo e sinalização de quando o fallback caiu no 503. Sem isso, quando o Gemini demora ou responde estranho, eu não sei dizer se foi rede, prompt ou modelo — com tracing, o span mostra o culpado em segundos.

---

## 2. Evolução — "como eu monitoro melhoria, e não só erro?"

**Pergunta:** *"Observabilidade serve só pra ver erro? Como eu acompanho se meu sistema com LLM está *melhorando* com o tempo (novo prompt, modelo novo, mais dados)?"*

**Resposta:** Duas frentes. **(1) Métricas operacionais** — latência, custo por chamada, tokens, taxa de error, taxa de timeout/fallback. Mostram *saúde*; mudam a cada deploy. **(2) Métricas de qualidade** — os **evals** rodados em produção ou em amostras: acurácia, taxa de recusa correta, alucinação detectada, score do LLM-as-judge. Mostram *eficácia*. A prática consolidada é **registrar o trace de cada chamada E o resultado do eval**, e montar **dashboards que comparam entre versões**: "prompt v2 melhorou acurácia em 4pts, mas custou 10% mais tokens". Assim abertura de prompt, troca de modelo ou ajuste de guardrail vira decisão guiada por dado — o mesmo princípio de controle de qualidade em QA tradicional.

**Por que interessa:** "monitorar" um sistema de LLM é responder duas perguntas em separado: *está de pé?* (ops) e *está bom?* (qualidade). Saber distingui-las — e propor dashboards para ambas — é a conversa de **LLMOps na prática**, e é exatamente o que um QA vira quando deixa de testar features e passa a testar **qualidade e custo de LLM em produção**.

**Exemplo meu (na prática):** eu sugeriria um painel duplo no meu app: **lado operacional** — % de chamadas ao Gemini com sucesso, tempo médio de resposta, quantas caíram no fallback (curva ao longo do tempo); **lado de qualidade** — numa amostra de triagens, quantas severidades bateram com o esperado (acurácia), quantas divergências apareceram (local × IA) e se as divergências foram justificadas. Prompts melhores = acurácia sobe; modelos mais lentos = custo/latência sobem. É assim que eu saberia — com número, não achismo — se vale seguir com o novo prompt.

---

*(Referência cruzada: conecta com `2026-09-04-evals-llm-qa.md` — evals são uma das duas frentes de LLMOps — e com `2026-08-29-mlops-cv-rag.md`, já que LLMOps é a evolução do MLOps clássico para aplicações com LLM.)*