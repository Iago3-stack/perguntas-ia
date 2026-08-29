# 2026-08-29 — MLOps, Computer Vision e RAG

**O que estudei hoje:** os 3 conceitos-chave que aparecem nas vagas de IA — e fui além do "o que é": questionei se eram só nomes novos pra coisas antigas.

---

## MLOps — Machine Learning Operations 🧠⚙️

Conceito: a "engenharia de produção" do ML — versionar modelos, treinar, testar, implantar e **monitorar** o modelo depois que ele está no ar (deriva de dados, retreino, acurácia caindo).

Minha dúvida: *"isso não é só DevOps com outro nome?"*
**Resposta honesta:** parcialmente. Ele reaproveita práticas que já existiam (versionamento, pipeline, CI). O que muda de real é o foco na **vida pós-treino** — manter o modelo saudável em produção, coisa que quase ninguém fazia. Aprox. 60% é formalizar o que já existia; 40% é problema genuinamente novo.

**Onde já toquei isso:** meu AI Bug Triage System tem **fallback automático entre modelos + resposta em JSON estruturado** — isso é sabor de MLOps (produção confiável, não só notebook).

---

## Computer Vision — Visão Computacional 👁️🤖

Conceito: ensinar máquinas a **enxergar** — classificar imagens, detectar objetos, ler documentos (OCR).

Minha dúvida: *"não é só label novo pra treinar modelo de imagem?"*
**Resposta honesta:** não. É um **domínio antigo da IA** (anos 60/70, antes dos LLMs) e é um **tipo de dado próprio** — o problema é sobre imagem, não texto. Técnicas específicas: convoluções, YOLO, OpenCV, OCR. Treinar já existia; a sigla é um domínio, não uma sigla nova.

---

## RAG — Retrieval-Augmented Generation 📂🧠

Conceito: antes de responder, o modelo **busca trechos relevantes numa base** (por significado) e responde **com base neles** — reduz alucinação e fundamenta a resposta.

Minha dúvida: *"chão vira token, mas não é só por busca?"*
**Resposta honesta:** o contrário do que imaginei. RAG é a técnica que **evita treinar**: em vez de retreinar o modelo pra falar do domínio (caro), ele **busca nos documentos na hora**. É método **novo que reduz treino**.

**Analogia do meu dia a dia administrativo:** como eu abrindo o arquivo do cliente antes de responder a pendência — "ir às pastas" em vez de chutar do que lembro.

---

## Ponto de vista

Estudar conceito não é decorar definição — é testar a **crítica** contra a explicação ("isso não é só relabeling?"). Ter a dúvida e buscar a resposta certa me ensina mais do que ler 20 linhas de verbete.