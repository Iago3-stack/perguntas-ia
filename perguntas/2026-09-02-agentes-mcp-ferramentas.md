# Agentes e MCP — 2 dúvidas rápidas resolvidas

## 1. Agente — "como ele 'faz' as coisas em outros sites (WhatsApp, YouTube)?"

**Pergunta:** *"Vi uma IA que acessava o WhatsApp Web, entrava no YouTube, pesquisava e tocava o vídeo. Como ela 'clica' nas coisas se é só um modelo de linguagem?"*

**Resposta:** O modelo em si **não clica** — ele **decide e delega**. O que a gente vê por trás é um agente rodando um loop: pega uma instrução em linguagem natural ("pesquisar X no YouTube e tocar") → **escolhe uma ferramenta disponível** (controlar mouse, digitar no campo de busca, apertar play) → chama essa ferramenta → **observa o resultado** (a tela mudou? o vídeo carregou?) → decide o próximo passo. O "braço" que realmente mexe no navegador é uma **automação de interface** (tipo o que faz o browser-digitado se mover e clicar); o LLM é só o "cérebro" que orquestra qual braço usar. Por isso dá pra controlar computador: não é magia do modelo, é **modelo + ferramentas de automação + loop**.

**Por que interessa:** desmistifica o "vírus mágico" que viraliza no LinkedIn. Entender que agente = cérebro + ferramentas + loop (e não um modelo novo que "aprende a usar o computador sozinho") é o que separa quem reproduz buzzword de quem sabe responder "como isso é possível" numa entrevista.

**Exemplo meu:** o meu motor de triagem tem uma função determinística `triar(descricao)`. Se eu embrulhar ela como ferramenta e der um objetivo em linguagem natural a um agente ("pega essa descrição e classifica a severidade"), quem executa é o mesmo motor — só que **orquestrado** pelo loop do agente, como se fosse um "vírus útil" controlado.

---

## 2. MCP — "sem MCP esse tipo de agente simplesmente não existe?"

**Pergunta:** *"Mas isso só funciona hoje porque existe MCP? Sem MCP não dava pra fazer?"*

**Resposta:** Dava — **mas o MCP é o que tornou isso barato e genérico**. Antes, para cada site/sistema que o agente precisasse controlar, você escrevia **uma integração manual e sob medida** (um código específico praquele site, com a manutenção de cada mudança de layout). Com MCP, a regra virou: **cada ferramenta vira um servidor MCP** que se declara (nome, o que faz, que parâmetros aceita) e qualquer agente **descobre e chama dinamicamente**, sem hardcode. Ou seja, MCP não criou o conceito de agente — criou o **padrão de encaixe** que faz o conceito escalar: o mesmo "cérebro" se conecta a qualquer "braço" que fale MCP, internet afora.

**Por que interessa:** a pergunta revela se o candidato sabe o que o MCP *realmente* resolve: não é "uma API nova", é o **contrato universal de ferramentas para agentes**. Saber diferenciar "feito à mão" de "padrão MCP" mostra maturidade de arquitetura.

**Exemplo meu (visão crítica de QA):** com meu app exposto como servidor MCP (`triar` e futuramente `gerar-casos-de-teste`), um agente de QA de qualquer empresa poderia plugá-lo direto — **sem ler meu código nem escrever integração**. É o cartão de visita que vira "periférico universal".

---

*(Referência cruzada: continuação de `2026-08-30-agentes-mcp.md` — mesmo tema, novas dúvidas práticas.)*
