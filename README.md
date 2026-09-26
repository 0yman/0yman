## Ayman Eldaly

**I build AI features that refuse to be confidently wrong.**

Final-year Data Science & AI student at Alexandria University, Egypt · ICPC (ECPC) qualifier ·
Looking for ML/AI Engineer roles · [0yman.github.io](https://0yman.github.io)

Most of what I build is a retrieval pipeline, an agent, or the evaluation harness
that decides whether either one is good enough to ship. Both test suites below run
offline with no API key, so the numbers are checkable rather than claimed.

The chunking, the hybrid retrieval, the rank fusion, the agent loop and the provider
adapters were written by hand first, because the interesting decisions live exactly
where a framework makes them quietly. Then the agent was rebuilt in LangGraph, and
tests hold both versions to identical answers.

---

### [ask-your-data](https://github.com/0yman/ask-your-data) · [live demo](https://ask-your-data-i67m.onrender.com)

Ask your data questions in plain English: drop in a CSV or Excel file, or use a
bundled dataset, and a tool-calling agent writes read-only SQL, runs it, checks that
every figure in its answer came from a query result, and shows the rows behind it and
every step. Visitors pick the model: Nemotron 3 Ultra or Ministral 14B.

- **Two engines, one behaviour.** The hand-written loop and a LangGraph state graph
  are held to identical answers, steps and tool calls by parity tests, and a paired
  evaluation scored them 17.0 and 16.7 of 17.
- **An MCP server.** Its read-only tools plug into Claude Desktop, Cursor or any MCP
  client, behind the same guardrails.
- **Guardrails are a control, not a request in a prompt.** `sqlglot` rejects stacked
  statements, DML hidden inside CTEs and DuckDB's file-read functions, over a
  connection that is read-only on its own.

What measuring it showed:

- A one-sentence prompt rule stopped the model inventing currency symbols, and cost
  **2.3 of 12** hard questions, because the model's SQL changed along with its wording.
  The fix moved into code, after the answer, where it cannot touch the queries.
- The same code scored anywhere from **8.3 to 10.7** on the hard set across sessions.
  Since then every change runs interleaved with the committed code in the same
  session, and only a gain that repeats counts.
- Execution accuracy on result sets, not SQL text: 0.944 answer accuracy and 1.000
  correct declines on questions the data cannot answer.

`Python` · `LangGraph` · `MCP` · `DuckDB` · `sqlglot` · `FastAPI` · `Docker` · 250 tests, no network, no API key

---

### [hybrid-rag-service](https://github.com/0yman/hybrid-rag-service)

Ask questions of your own PDFs and notes, and see exactly which passage each
answer came from. Double-click to run, no API key needed. Under the hood: FAISS
dense retrieval and BM25 fused with Reciprocal Rank Fusion, citations validated
against the passages they point at, and a plain "not in your documents" when
the answer isn't there.

The evaluation is the actual project, and it kept contradicting me:

- Dense retrieval dropped to **0.667 to 0.800 recall@3** on keyword queries, where
  BM25 scored 1.000. At k=3, BM25 alone was the safest retriever, not the hybrid
  I'd built.
- Swapping the embedding runtime for a 10× smaller install was meant to be
  packaging. The "same" model produced different vectors and moved recall **13
  points**.
- CI scored differently from my laptop, with identical code. Rank-fusion ties
  were being broken by *absolute file paths*.

Each one is written up, with the fix, in the README.

`Python` · `FAISS` · `BM25` · `ONNX Runtime` · `FastAPI` · `Docker` · 161 tests, no network, no API key

---

### Now

**AYD-0.1**, a 9B SQL agent model: fine-tuning Qwen3.5-9B on agent conversations
that a 27B teacher produced and that were kept only when their final result matched
the gold result. Trained and measured on free Kaggle GPUs. Numbers go here once they
are measured.

### Working with

Python · SQL · RAG & hybrid retrieval · tool-calling agents · LangGraph · MCP ·
OpenAI, Gemini and OpenAI-compatible APIs · vLLM · offline evaluation (recall@k, MRR,
nDCG, execution accuracy, paired A/B runs) · scikit-learn · FastAPI · Docker · GitHub Actions

Previously: AI engineering intern at Alexandria Port Authority, working on
800,000+ maritime logistics records.

[aymaneldaly72@gmail.com](mailto:aymaneldaly72@gmail.com) · [LinkedIn](https://linkedin.com/in/ayman-eldaly) · [Portfolio](https://0yman.github.io)
