# Embeddings & Banco Vetorial — 2 dúvidas que todo mundo ignora

## 1. Embeddings — "não é só transformar palavra em número?"

**Pergunta:** *"Embeddings não são uma tabela simples de 'palavra → número'? O que tem de especial?"*

**Resposta:** Não é uma tabela rasa. Embeddings são **vetores densos de alta dimensionalidade** onde palavras com **significado parecido ficam perto umas das outras** num espaço matemático. Diferente de uma codificação simples (onde cada palavra vira um número isolado, sem relação), embeddings **capturam semântica e contexto**: "triste" e "infeliz" ficam próximos; "triste" e "carro" ficam longe. Essa propriedade é o que torna possível a **busca semântica** (encontrar algo pelo sentido, não pela palavra exata) — e é exatamente a base de um RAG.

**Por que interessa:** sem embeddings, um sistema de busca só encontra termos idênticos ao que o usuário digitou. Com embeddings, ele **entende o que o usuário quis dizer** — e busca trechos com sentido parecido mesmo que as palavras sejam diferentes.

**Exemplo meu:** o meu motor de triagem hoje usa léxico (palavras-chave = pesos). Se algum dia evoluir pra busca semântica nos tickets de bug, embeddings são o próximo passo natural.

---

## 2. Banco vetorial — "não posso só salvar os vetores no Postgres que já tenho?"

**Pergunta:** *"Se já tenho PostgreSQL, preciso de um banco vetorial separado pra RAG?"*

**Resposta:** Pode — e pra volume pequeno, funciona bem (extensão **pgvector** do PostgreSQL salva vetores e faz busca). O que muda em bancos vetoriais especializados (Pinecone, Qdrant, Weaviate, Milvus) são **estruturas de indexação feitas pra alta dimensionalidade** (HNSW, IVF): buscam milhões de vetores em milissegundos, algo que o B-tree tradicional não faz. A escolha é de escala: pra um repo com dezenas a poucas centenas de documentos, pgvector basta; pra milhões, banco vetorial dedicado.

**Por que interessa:** essa é uma decisão de arquitetura clássica — "basta o que eu já tenho ou preciso de infra nova?" — que aparece em entrevista e desenhos de sistema. Saber responder mostra que não está só montando RAG de tutorial.

**Analogia do meu dia a dia (Auxiliar Administrativo):** indices no arquivo físico funcionam bem pra poucos processos; quando a pilha cresce muito, a gente separa um arquivo专门 pra consulta rápida (mais organizado, indexado de outro jeito). É a mesma lógica.