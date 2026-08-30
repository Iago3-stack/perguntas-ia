# Agentes e MCP — 3 dúvidas resolvidas

## 1. MCP — "não é só uma API com nome novo?"

**Pergunta:** *"MCP (Model Context Protocol) não é só reinventar o que as APIs já faziam?"*

**Resposta:** Não — é **uma camada acima das APIs**. API é o contrato de um software específico: você sabe que existe `/criar-bug`, lê a documentação e chama. MCP é o **padrão de integração para agentes**: o servidor MCP **expõe ferramentas** (tools) e o cliente MCP (um agente, uma IDE) **descobre e chama essas ferramentas dinamicamente**, no meio da conversa. É o famoso "padrão USB-C da IA" — você conecta qualquer cabeça (LLM) a qualquer periférico (a sua ferramenta), sem plug exclusivo de cada um.

**Por que interessa:** quando um produto anuncia "suporte a agentes", hoje isso quase sempre significa "fala MCP". A conversa do ecossistema migrou de *"qual API?"* para *"qual protocolo"* — e MCP ganhou como padrão de fato, com adoção cruzada entre os grandes provedores.

**Exemplo meu:** o meu motor de triagem expõe hoje uma função determinística (`triar(descricao)`). Embrulhar essa mesma função como **ferramenta de um servidor MCP** transforma o app num periférico que qualquer agente pode usar — sem ninguém precisar saber meu código.

---

## 2. Agente — "o que faz uma IA ser 'agente' hoje?"

**Pergunta:** *"Todo mundo fala em agentes de IA. O que exatamente separa um agente de um chat comum?"*

**Resposta:** O **loop**. Um chat recebe pergunta → devolve texto. Um agente recebe um **objetivo em aberto** e executa um ciclo: interpretar o pedido → **escolher uma ferramenta** → chamar → **observar o resultado** → decidir o próximo passo... até concluir. A diferença quase nunca está no modelo — está em **ter ferramentas e poder agir**. Sem MCP, cada ferramenta exigiria integração manual e individual (um agente "fútil" funciona só pra H de um sistema). Com MCP, o loop do agente vira genérico e as ferramentas viraram periféricos plugáveis.

**Por que interessa:** quem ainda acha que "agente é inventar tipo novo de modelo" vai errar entrevista; quem enxerga "agente = modelo + loop + ferramentas" sabe exatamente o que construir. É a diferença entre consumir IA e operar IA.

**Cenário meu (QA):** um agente de QA poderia pegar um ticket de bug → **classificar a severidade** (ferramenta de NLP) → **buscar o histórico** no Jira (outra ferramenta via MCP) → **gerar o Gherkin** pronto pra copiar. Cada passo é uma ferramenta; o agente é quem orquestra.

---

## 3. MCP — "isso serve pro meu nível ou é só coisa de empresa gigante?"

**Pergunta:** *"MCP parece infraestrutura de big tech. Vale pra um dev/QA que está começando em IA?"*

**Resposta:** Vale — e é um dos caminhos mais baratos de demonstrar IA de aplicação. Um servidor MCP pode ser um **arquivo Python pequeno** que expõe funções do seu próprio app. Você roda local (entrada/saída padrão), testa com o **cliente MCP/client da linha de comando** e conecta em qualquer cliente MCP que rodo na sua máquina. Não precisa de nuvem, cluster nem licença — precisa só de uma função útil pra expor.

**Por que interessa:** vagas de *agentes de IA* vêm crescendo (vi até vaga de "Agentes IA") e quase todas perguntam por MCP. Ter **um repositório mostrando um servidor MCP real** — com ferramentas de triagem de bug, por exemplo — prova a diferença entre "leu sobre" e "já conecta IA a dados".

**Próximo passo no meu lab Hack28:** expor o motor de triagem como servidor MCP (stdio), testar com um cliente MCP e documentar no GitHub — transformando o app de vitrine em **periférico de agentes**.