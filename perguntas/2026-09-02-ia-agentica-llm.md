# IA Agêntica × LLM — 2 dúvidas resolvidas (com exemplo do "Zeca" de navegador)

## 1. LLM — "agora todo mundo chama de IA. LLM não é só IA com nome bonito?"

**Pergunta:** *"Falam 'isso usa LLM', 'aquilo é uma LLM'... Mas LLM não é só o ChatGPT com outro nome? O que é um LLM de verdade?"*

**Resposta:** **LLM (Large Language Model)** é o **modelo de linguagem** — o "cérebro" que aprendeu bilhões de padrões de texto e, dado um pedido, **prevê a próxima palavra/token** pra gerar uma resposta. Ele **não executa nada no mundo real**: lê texto e devolve texto. O ChatGPT é um **produto** construído sobre um LLM (GPT) + interface. Então a hierarquia é: *LLM* (o motor) → *Chatbot/chat* (o LLM envolto em conversa) → *Agente* (o LLM + objetivo + ferramentas + loop). O termo "IA" é o guarda-chuva; LLM é uma **tecnologia específica** dentro dela — não é sinônimo.

**Por que interessa:** quem entende que LLM é **só o motor de raciocínio** já não confunde "colocar um modelo" com "construir um sistema". Em entrevista, essa distinção separa quem fala buzzword de quem sabe que o modelo sozinho **não tem mãos nem feedback** — não consegue consultar um banco, abrir arquivo ou verificar se acertou.

**Exemplo meu:** no meu motor de triagem, a análise por IA (Gemini) é um **LLM**: ele recebe a descrição do bug e devolve um JSON com severidade/causa raiz. Mas **quem executa** (recebe o texto, chama a API, trata o fallback, monta o relatório) é o **código em volta** — o LLM é só o cérebro que raciocina sobre o texto.

---

## 2. IA Agêntica — "não é só o LLM que usa ferramentas?"

**Pergunta:** *"Vi uma IA que acessava o WhatsApp Web, entrava no YouTube, pesquisava e tocava o vídeo. Isso não é só o mesmo LLM com um pouco mais de código? Por que chamam de 'IA agêntica'?"*

**Resposta:** Porque "agente" não é "LLM com ferramenta" — é **LLM + um loop onde ele age e reage**. A fórmula que todo framework usa (ReAct, OODA e afins):

> **Agente = LLM (cérebro) + objetivo + ferramentas (mãos) + memória + LOOP**

O loop é o que define um agente: **perceber → planejar → agir (chamar ferramenta) → observar o resultado → decidir se termina ou repete**. O LLM decide o próximo passo, mas quem **mexe no navegador/clica/pesquisa/apertar play** é a **ferramenta** (automação de interface). A "IA Agêntica" é esse paradigma em que o modelo deixa de *responder* e passa a *executar tarefas de múltiplos passos por conta própria*. Removendo o loop e as ferramentas, volta a ser um chatbot de resposta única.

**Por que interessa:** é a pergunta que separa **generative AI** (gera uma saída) de **agentic AI** (age até concluir). Saber que "agente = LLM + objetivo + ferramentas + loop" responde o "como a IA controla o computador?" sem cair na ideia mágica — e mostra maturidade pra falar de arquitetura de verdade.

**Exemplo meu (QA, o "Zeca de testes"):** imagine um agente de QA com um loop: **recebe** o ticket de bug → **chama** a ferramenta de NLP (meu `triar`) pra classificar severidade → **busca** o histórico no Jira (outra ferramenta via MCP) → **gera** o Gherkin e **abre** a issue. Cada passo é uma ferramenta; quem **orquestra o ciclo** é o agente; o LLM raciocina em cada etapa. O mesmo princípio da IA que toca vídeo no YouTube — só que com ferramentas de QA.

---

*(Referência cruzada: conecta com `2026-08-30-agentes-mcp.md` — agentes/ferramentas/MCP — e com a IA "Zeca" de controle de navegador vista em 2026-09.)*
