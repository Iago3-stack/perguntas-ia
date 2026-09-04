# Function Calling & Tools — 2 dúvidas que ligam o agente ao mundo real

## 1. Function calling — "não é só o LLM devolvendo um JSON?"

**Pergunta:** *"Dizem que o agente 'chama uma função'. Mas na prática não é só o modelo responder com um JSON e o meu código tratar? O que tem de tão especial?"*

**Resposta:** É quase isso — mas a parte que comuteia a travar todo mundo é que **o LLM não executa nada**: ele *propõe* a chamada. O mecanismo (function calling) funciona assim: você declara as ferramentas disponíveis com um **schema** (nome, descrição e parâmetros em JSON Schema), o modelo lê o pedido do usuário, decide qual ferramenta é adequada e devolve **apenas a intenção** — um JSON com `tool_call` contendo o nome da função e os argumentos. **Quem executa é o seu código** (a runtime), e o resultado da execução retorna ao modelo como mais uma mensagem, para ele continuar o raciocínio. Esse "eu proponho, você executa, o resultado volta" é o coração do loop agêntico — e é também o que impede o modelo de "sair agindo" sozinho sem o seu controle.

**Por que interessa:** entender que o modelo *sugere* e o código *autoriza* responde a pergunta de segurança que todo mundo faz: "a IA pode fazer qualquer coisa?". Não — sem uma runtime que execute, o LLM é só um texto dizendo *"chama a função X com esses args"*. Saber separar **decisão** (modelo) de **execução** (código) mostra maturidade para desenhar agentes e falar de arquitetura em entrevista.

**Exemplo meu (MCP server de QA):** no meu provedor de conceito de servidor MCP, cada ferramenta (ex: `triar` via NLP, buscar ticket no Jira) é declarada com schema. O agente recebe o relato de bug e o Gemini devolve `{"tool_call": {"name": "triar", "arguments": {"descricao": "não consigo pagar"}}}`. **Meu código** é que de fato roda `triagem.py`, pega a gravidade, anexa o resultado à conversa — e aí sim o modelo decide o próximo passo. Quem tem mãos é a runtime; o LLM só aponta o caminho.

---

## 2. Escolha da ferramenta — "se o LLM escolhe, quem manda no final?"

**Pergunta:** *"Se o modelo decide qual ferramenta chamar, não é ele que está no controle? Como eu garanto que ele não chama a ferramenta errada ou em loop infinito?"*

**Resposta:** O LLM *sugere*, mas **você define as regras do jogo** em três níveis: **(1) o que existe** — só as ferramentas que você registrar no schema ficam disponíveis (nada além disso); **(2) como ele escolhe** — parâmetro `tool_choice`: forçar uma tool específica, permitir que o modelo escolha livremente, ou nem oferecer tools ("none"); e **(3) o que é autorizado** — a runtime pode validar argumentos, checar permissões e recusar antes de executar. Para loops infinitos, frameworks usam **limite de iterações** e **máximos de passos**: o loop para quando atinge o teto, e você recebe o caminho percorrido (trace) para auditar. Ou seja: controle fica em código — o modelo é um orquestrador confinado dentro das regras que você definiu.

**Por que interessa:** é a pergunta de **governança de agentes**. Saber responder "quem manda: o modelo ou o sistema?" com "o sistema define o espaço de ação, o modelo escolhe dentro dele" mostra que você não está só amarrando LLMs — está **desenhando limites e salvaguardas**, que é exatamente o papel de QA em sistemas agenticos.

**Exemplo meu (QA, na prática):** se eu ligar o agente "Zeca" ao Jira via MCP, eu limito: `tool_choice` só permite `buscar_ticket` e `criar_issue` (nada de "deletar" ou "alterar status"), valido que a descrição não esteja vazia antes de chamar a API, e coloco `max_iterations=5` — se o agente tentar dar mais de 5 passos sem concluir, o loop encerra e loga o trace. O modelo é livre pra explorar, mas dentro da cerca que eu construí — e é essa cerca que define a segurança do sistema.

---

*(Referência cruzada: conecta com `2026-08-30-agentes-mcp.md` e `2026-09-02-agentes-mcp-ferramentas.md` — MCP expõe as ferramentas que o function calling invoca — e com `2026-09-02-agentes-ia-llm.md`, o loop agêntico que motiva essa troca de mensagens.)*