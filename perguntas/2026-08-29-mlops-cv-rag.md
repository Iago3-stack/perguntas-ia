# MLOps, Computer Vision e RAG — 3 dúvidas resolvidas

## 1. MLOps — "não é só DevOps rebatizado?"

**Pergunta:** *"MLOps não é só o que o DevOps já fazia, com um nome novo?"*

**Resposta:** Em parte, sim — com ressalvas. MLOps reaproveita práticas que já existiam em engenharia de software: versionamento, pipelines, CI/CD, observabilidade. O que ele formaliza de **novo** é o foco na **vida do modelo depois do treino**: monitoramento de deriva de dados, retreino, queda de acurácia em produção. Aproximadamente 60% é organização do que já existia; 40% é problema genuinamente novo (o modelo não é código que "termina de entregar").

**Por que interessa:** na prática, colocar IA confiável em produção é o gargalo número 1 das empresas. Um candidato que conhece fallback, JSON estruturado e tratamento de falha já demonstra "sabor de MLOps".

**Exemplo meu:** o AI Bug Triage System usa **fallback automático entre modelos** e **resposta em JSON estruturado** — produção mais confiável, não só notebook.

---

## 2. Computer Vision — "não é só label novo pra treinar imagem?"

**Pergunta:** *"Treinar modelos de imagem já existia; CV não é só empacotar isso num nome?"*

**Resposta:** Não. Visão computacional é **domínio antigo da IA** (anos 60/70, bem antes dos LLMs) e representa um **tipo de dado próprio**: o problema é sobre **imagem**, não texto. Técnicas específicas do domínio — convoluções, detecção de objetos (YOLO), OCR, OpenCV — não são "sigla nova"; são a área. Treinar já existia, mas CV é onde o treino acontece, não como.

**Por que interessa:** quem entende que CV é domínio (e não método) sabe ler uma vaga que pede OCR/IDP e enxergar a arquitetura certa. Junto com NLP, forma o eixo "máquina lê o mundo" (texto → olhos).

---

## 3. RAG — "não é só ligar por busca com outro nome?"

**Pergunta:** *"Se eu já posso treinar/fine-tuning o modelo pro domínio, RAG não é só dar nome bonito pra 'colocar dados'?"*

**Resposta:** É o **contrário** — e essa é a parte que contraria o senso comum. RAG é a técnica que **evita treinar**: em vez de retreinar um modelo pra falar do domínio da empresa (caro e arriscado), ele **busca trechos relevantes numa base na hora de responder** e fundamenta a resposta neles (menos alucinação, resposta rastreável). Ou seja: é método **novo que reduz a necessidade de treino**, não um novo nome pra treino.

**Por que interessa:** o par fine-tuning × RAG é decisão arquitetural real em todo produto com LLM. Quem consegue explicar a diferença mostra que não está "decorando siglas".

**Analogia do meu dia a dia (Auxiliar Administrativo):** antes de responder uma pendência, eu abro o arquivo do cliente e busco o histórico — em vez de responder de cabeça o que eu lembro. Isso é RAG: ir às pastas antes de responder.