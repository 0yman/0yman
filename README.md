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

Ask questions of your own PDFs and notes, and see exactly which passage each
answer came from. Double-click to run, no API key needed. Under the hood: FAISS
dense retrieval and BM25 fused with Reciprocal Rank Fusion, citations validated
against the passages they point at, and a plain "not in your documents" when
the answer isn't there.

The evaluation is the actual project, and it kept contradicting me:

- Dense retrieval dropped to **0.667–0.800 recall@3** on keyword queries, where
  BM25 scored 1.000 — and at k=3, BM25 alone was the safest retriever, not the
  hybrid I'd built.
- Swapping the embedding runtime for a 10× smaller install was meant to be
  packaging. The "same" model produced different vectors and moved recall **13
  points**.
- CI scored differently from my laptop, with identical code. Rank-fusion ties
  were being broken by *absolute file paths*.

Each one is written up, with the fix, in the README.

`Python` · `FAISS` · `BM25` · `ONNX Runtime` · `FastAPI` · `Docker` · 161 tests, no network, no API key

---

### [ask-your-data](https://github.com/0yman/ask-your-data)

Ask your data questions in plain English: drop in a CSV or Excel file (or use
the built-in port warehouse) and a tool-calling agent writes read-only SQL,
runs it, and shows the answer, the rows behind it, and every step. Double-click
to run; the page walks you through adding a free AI key.

Guardrails are a control, not a request in a prompt: `sqlglot` rejects stacked
statements, DML hidden inside CTEs, and DuckDB's file-read functions — the real
exfiltration path — over an independently read-only connection.

Evaluated by **execution accuracy on result sets, not SQL text**: 0.944
end-to-end answer accuracy, and 1.000 correct declines on questions the warehouse
genuinely cannot answer. An ablation found that putting the schema in the system
prompt uses **5% fewer** prompt tokens than letting the agent discover it — the
opposite of what I expected, and the reason I measure instead of guessing.

`Python` · `OpenAI & Gemini function calling` · `DuckDB` · `sqlglot` · 136 tests, no network, no API key

---

### Working with

Python · SQL · RAG & hybrid retrieval · tool-calling agents · OpenAI and Gemini
APIs · offline evaluation (recall@k, MRR, nDCG, execution accuracy) ·
scikit-learn · FastAPI · Docker · GitHub Actions

Previously: AI engineering intern at Alexandria Port Authority, working on
800,000+ maritime logistics records.

📫 aymaneldaly72@gmail.com · [LinkedIn](https://linkedin.com/in/ayman-eldaly)
