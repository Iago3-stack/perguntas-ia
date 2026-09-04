# Evals & Avaliação de LLM — 2 dúvidas que ninguém responde direito

## 1. Evals — "não é só rodar o teste e ver se passou?"

**Pergunta:** *"'Avaliar o LLM' soa como 'rodar os testes e ver se a resposta está certa'. Não é só unit test com nome bonito? O que tem de diferente?"*

**Resposta:** Parece, mas não é. Evals (evaluations) é um **processo sistemático de medir a qualidade de um modelo ou de um sistema que usa o modelo**, e a diferença está no **objeto da avaliação e no jeito de julgar**. Num unit test clássico, o resultado é **determinístico**: entrou 2 + 2, saiu 4 — é fixo. Com LLM, a saída é **probabilística**: o mesmo prompt pode gerar respostas diferentes a cada chamada. Então o "teste" deixa de ser "comparar com o esperado exato" e vira **"avaliar se a resposta cumpre o critério"** — pode ser via métrica automática (exact match, F1, cosine similarity, BLEU/ROUGE) ou via **LLM-as-judge** (um segundo modelo avaliando a resposta do primeiro). E evals não roda uma vez: vira um **conjunto de testes (evaluation set/golden set)** que você atualiza conforme o sistema evolui, pra pegar **regressões** — exatamente como um suite de testes de QA tradicional.

**Por que interessa:** é o ponto onde QA de software e QA de IA se encontram. Saber dizer "eu não confio no output do modelo por confiar — eu meço" é o que separa quem só *usa* LLM de quem **engenheira** com LLM. Todo pipeline sério (triagem, RAG, agente) precisa de evals, porque o modelo muda de versão, o prompt muda, os dados mudam — e sem evals você descobre a regressão *depois* de quebrar em produção.

**Exemplo meu:** no meu motor de triagem, o critério automático já existe na parte determinística (NLP) — eu sei *exatamente* qual severidade cada bug recebe. O desafio é avaliar o **fallback com Gemini**: montar um **golden set** de bugs já classificados e comparar a severidade que o Gemini devolveu com a esperada (exact match da severidade + F1 das categorias de causa raiz), e usar **LLM-as-judge** pra julgar se a *justificativa* da causa raiz faz sentido em PT-BR.

---

## 2. Confiar no output — "como eu sei que o modelo não está só me enganando?"

**Pergunta:** *"Posso ler a resposta e achar que está boa. Mas como eu sei, de forma objetiva, que o meu LLM acertou de verdade — e não só me convenceu?"*

**Resposta:** Você não confia na leitura individual — você **mede sobre um conjunto de exemplos conhecidos**. A abordagem padrão: **golden set** (um conjunto curado de entradas com a resposta/desfecho esperado), onde você roda o sistema, compara cada saída com o esperado e agrega em **métricas** (acurácia, precision, recall, F1 para classificação; exact match ou ROUGE/BLEU para texto; e/ou score do LLM-as-judge com critérios explícitos). Isso dá um **número comparável entre versões**: se eu troco o modelo ou o prompt, a métrica sobe ou desce. E tem um detalhe crítico: **o judge também é um modelo**, então ele mesmo pode errar ou ter viés — por isso quanto mais o critério pode ser **objetivo/automático** (checar severidade == "alta"), mais confiável, e o LLM-as-judge fica só para o que é subjetivo (qualidade do texto, relevância da justificativa).

**Por que interessa:** "me convenceu" não é métrica. Em produção, gasto de token, latência e retrabalho dependem de o modelo *acertar* na primeira — e a única forma de provar é mostrando um **número antes/depois**. Em entrevista, falar de "golden set + F1 + LLM-as-judge" mostra que você pensa em **qualidade de modelo como engenheiro**, não como usuário.

**Exemplo meu (QA, na prática):** se eu quero validar o meu fallback de IA no triagem, eu pego, digamos, **30 bugs reais** com severidade esperada já acertada pelo meu motor NLP determinístico, rodo o Gemini neles e comparo: quantas vezes a severidade bateu (exact match), como a categoria de causa raiz se distribuiu (precision/recall por categoria), e uso um prompt de judge perguntando "a justificativa está coerente com a descrição do bug?" com resposta sim/não + nota. Resultado: um **painel** tipo "F1 = 0.87, acurácia = 90%, judge aprova 95% das justificativas". É isso que define se o fallback é seguro de ativar ou não.

---

*(Referência cruzada: conecta com `2026-09-02-agentes-ia-llm.md` — o LLM como "motor de raciocínio" que não tem mãos — e com `2026-08-31-fine-tuning-json-estruturado.md`, já que evals são o que mede se o prompt/fine-tune realmente melhorou a saída JSON.)*
