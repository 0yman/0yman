## Ayman Eldaly

**I build AI features that refuse to be confidently wrong.**

Data Science & AI senior at Alexandria University, Egypt · ICPC (ECPC) qualifier ·
Looking for ML/AI Engineer roles.

Most of what I build is a retrieval pipeline, an agent, or the evaluation harness
that decides whether either one is good enough to ship. Both projects below run
offline with no API key, so the numbers are checkable rather than claimed.

Neither uses an agent framework. The chunking, the hybrid retrieval, the rank
fusion, the agent loop, the tool dispatch and the provider adapters are all
written out — partly because the interesting decisions live exactly where a
framework would have made them for me.

---

### [hybrid-rag-service](https://github.com/0yman/hybrid-rag-service)

Retrieval-augmented QA. FAISS dense retrieval and BM25 fused with Reciprocal Rank
Fusion, citations validated against the passages they point at, and abstention
when the corpus does not support an answer.

The evaluation is the actual project. Scoring two query distributions separately
showed dense retrieval **collapsing from 0.935 to 0.667 recall@3** on keyword
queries — where BM25 scored 1.000. The hybrid fusion I had assumed was a clear
win came second on *both* sets. I reported that instead of tuning the benchmark
until it agreed with me.

`Python` · `FAISS` · `BM25` · `FastAPI` · `Docker` · 100 tests, no network, no API key

---

### [port-analyst-agent](https://github.com/0yman/port-analyst-agent)

A tool-calling agent that answers analytical questions by writing read-only SQL
against a DuckDB star schema, with a bounded reasoning loop, self-correction on
query errors, and a full trace of every tool call and token.

Guardrails are a control, not a request in a prompt: `sqlglot` rejects stacked
statements, DML hidden inside CTEs, and DuckDB's file-read functions — the real
exfiltration path — over an independently read-only connection.

Evaluated by **execution accuracy on result sets, not SQL text**: 0.944
end-to-end answer accuracy, and 1.000 correct declines on questions the warehouse
genuinely cannot answer. An ablation found that putting the schema in the system
prompt uses **5% fewer** prompt tokens than letting the agent discover it — the
opposite of what I expected, and the reason I measure instead of guessing.

`Python` · `OpenAI & Gemini function calling` · `DuckDB` · `sqlglot` · 115 tests, no network, no API key

---

### Working with

Python · SQL · RAG & hybrid retrieval · tool-calling agents · OpenAI and Gemini
APIs · offline evaluation (recall@k, MRR, nDCG, execution accuracy) ·
scikit-learn · FastAPI · Docker · GitHub Actions

Previously: AI engineering intern at Alexandria Port Authority, working on
800,000+ maritime logistics records.

📫 aymaneldaly72@gmail.com · [LinkedIn](https://linkedin.com/in/ayman-eldaly)
