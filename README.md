<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=D%C3%BAvidas%20de%20IA%20e%20QA&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

> 🌐 *English readers: this document is in PT-BR, but your browser can translate it automatically (right-click → "Translate").*

> 🧠 *(O lab onde a minha confusão vira conteúdo — e a sua dúvida vira o próximo capítulo.)*

IA mudou de geração: hoje não se pergunta *"o que é"*, mas *"isso não é só coisa que já existia com outro nome?"* — MLOps, RAG, agentes, embeddings, fine-tuning... Cada "sigla nova" parece enfeite até a hora que você precisa decidir de verdade.

Este repositório é o meu **caderno público de resolver essas dúvidas sem decoreba**: eu registro a pergunta do jeito que todo dev se faz, dou a resposta direta e mostro **onde aquilo aparece em produção** — e quando cabe, coloco um exemplo do que eu mesmo construo.

<div align="center">
  <a href="https://github.com/Iago3-stack/perguntas-ia/stargazers">
    <img src="https://img.shields.io/github/stars/Iago3-stack/perguntas-ia?style=for-the-badge&color=2E7CF6&logo=github&logoColor=white&label=Estrelas" />
  </a>
</div>

> ⭐ **Se essa curadoria te ajudou, dá uma estrelinha no repo** — quanto mais estrelas, mais devs encontram as respostas na busca do GitHub. É de graça!

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=A%20Curadoria&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

Coleção de perguntas técnicas de **IA e QA Automation** que resolvi e documentei. Cada entrada tem:

- 🧠 **Pergunta** — formulada como todo dev se faz (inclusive a "essa pergunta é só enfeite?")
- ⚡ **Resposta direta** — conceito, de forma enxuta
- 🎯 **Por que interessa** — contexto e onde a coisa aparece em produção

Nada de verbete decorado: por trás de cada resposta há **dúvida de verdade** e **exemplo prático** (com código real quando couber).

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=%C3%8Dndice&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

<div align="center">
  <img src="https://img.shields.io/badge/8%20cap%C3%ADtulos-4CAF50?style=for-the-badge" />
  <img src="https://img.shields.io/badge/14%20d%C3%BAvidas%20resolvidas-2E7CF6?style=for-the-badge" />
</div>

| Tema | Pergunta central |
|---|---|
| [MLOps](perguntas/2026-08-29-mlops-cv-rag.md) | "MLOps não é só DevOps rebatizado?" |
| [Computer Vision](perguntas/2026-08-29-mlops-cv-rag.md) | "CV não é só label novo pra treinar imagem?" |
| [RAG](perguntas/2026-08-29-mlops-cv-rag.md) | "RAG não é só correspondência com outro nome?" |
| [Agentes & MCP](perguntas/2026-08-30-agentes-mcp.md) | "MCP não é só uma API com nome novo?" |
| [Embeddings & Banco Vetorial](perguntas/2026-08-31-embeddings-vectordb.md) | "Embeddings não é só 'palavras viradas número'?" |
| [Fine-tuning & JSON Estruturado](perguntas/2026-08-31-fine-tuning-json-estruturado.md) | "Fine-tuning não é só treinar com meus dados?" |
| [Agentes & MCP (cont.)](perguntas/2026-09-02-agentes-mcp-ferramentas.md) | "Como um agente 'clica' em outros sites?" |
| [IA Agêntica × LLM](perguntas/2026-09-02-ia-agentica-llm.md) | "IA agêntica não é só o LLM que usa ferramentas?" |

> Cada pergunta entra aqui conforme é estudada e **resolvida** — o valor está em registrar a pergunta certa, não a definição pronta.

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=Temas%20em%20Foco&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

<div align="center">
  <img src="https://img.shields.io/badge/MLOps-2E7CF6?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Computer%20Vision-9C27B0?style=for-the-badge" />
  <img src="https://img.shields.io/badge/RAG-4CAF50?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Agentes%20%26%20MCP-FF4B4B?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Embeddings-FF9800?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Fine-tuning-00ACC1?style=for-the-badge" />
  <img src="https://img.shields.io/badge/QA%20Automation-25D366?style=for-the-badge" />
</div>

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=Estrutura&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

| Caminho | Papel |
|---|---|
| 📖 `perguntas/` | Capítulos de curadoria — um arquivo por dia/tema |
| 🧭 `README.md` | Índice e nota de curadoria (este arquivo) |

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=Tem%20uma%20D%C3%BAvida%3F&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

Abra um [issue](https://github.com/Iago3-stack/perguntas-ia/issues) com a sua pergunta de IA/QA — a resposta vira o próximo capítulo desta curadoria.

<div align="center">
  <a href="https://github.com/Iago3-stack/perguntas-ia/issues/new">
    <img src="https://img.shields.io/badge/Abrir%20Issue-2E7CF6?style=for-the-badge&logo=github&logoColor=white" />
  </a>
</div>

---

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&customColorList=20,24,25&height=64&section=header&text=Licen%C3%A7a%20e%20Autoria&fontSize=24&fontColor=fff&fontAlignY=58" width="100%" />
</div>

<div align="center">
  <a href="CHANGELOG.md"><img src="https://img.shields.io/badge/Changelog-4CAF50?style=for-the-badge&logo=github&logoColor=white" /></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/Licen%C3%A7a-Apache2.0-4CAF50?style=for-the-badge&logo=apache&logoColor=white" /></a>
  <img src="https://img.shields.io/badge/Autor-Iago%20Nunes-2E7CF6?style=for-the-badge&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/GitHub-Iago3%20stack-181717?style=for-the-badge&logo=github&logoColor=white" />
</div>

**🧑‍💻 Autor:** [Iago Nunes (Iago3-stack)](https://github.com/Iago3-stack) — QA Automation Engineer | Estudante de IA & Machine Learning na UNIASSELVI.

🕓 A curadoria cresce conforme estudada, com **data e tema em cada capítulo**, tudo público em [github.com/Iago3-stack/perguntas-ia](https://github.com/Iago3-stack/perguntas-ia).
