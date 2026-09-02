# Fine-tuning & JSON Estruturado — 2 decisões de quem coloca IA em produção

## 1. Fine-tuning — "não é só treinar com meus dados?"

**Pergunta:** *"Fine-tuning não é só pegar um modelo e treinar com os dados da empresa pra ele ficar especialista?"*

**Resposta:** É parecido, mas **não é só treinar** — é **modificar os pesos internos** do modelo com um conjunto de dados curado. O custo é alto (tempo de GPU, dados limpos, risco de "esquecimento catastrófico" quando o modelo perde conhecimento geral) e o resultado é uma mudança de **comportamento/formatação**, não de conhecimento factual que muda todo dia. Fine-tuning é ideal pra fazer o modelo responder num **estilo**, **formato** ou **tom** específicos — mas pra informações atualizadas, RAG é mais prático e barato.

**Por que interessa:** essa é uma das decisões arquiteturais mais cobradas em vagas de IA de aplicação. Saber dizer *"fine-tuning pra comportamento; RAG pra conhecimento"* prova que entende a diferença entre "decorar" e "usar".

**Exemplo meu:** o meu motor de triagem usa um modelo pré-treinado com regras fixas — não preciso de fine-tuning porque o comportamento já é determinístico. Se algum dia quiser que o modelo responda num tom "suave" ou "técnico" pro usuário final, aí sim fine-tuning faria sentido.

---

## 2. JSON estruturado — "por que forçar o LLM a retornar JSON?"

**Pergunta:** *"Se o modelo responde bem em texto livre, por que forçar ele a devolver JSON com chaves específicas?"*

**Resposta:** Porque em **produção**, texto livre é impossível de processar automaticamente. Quando você força o retorno a seguir um schema JSON (com chaves como `gravidade`, `sentimento`, `fatores`), o código que consome essa resposta **sabe exatamente onde ler** — sem regex, sem parse manual, sem quebra. Ferramentas como **Pydantic**, **function calling** dos provedores e **constrained decoding** existem justamente pra isso: garantir que a resposta do LLM é parseável e confiável.

**Por que interessa:** todo pipeline de IA sério usa JSON estruturado. Quando você demonstra que o seu app já gera JSON estruturado com Gemini, mostra que pensa em **produção**, não só em notebook.

**Exemplo meu:** o AI Bug Triage System pede ao Gemini que retorne `{"gravidade": "...", "sentimento": "...", "fatores": [...]}` — se fosse texto livre, o app teria que adivinhar onde termina a resposta e onde começa a lixeira.