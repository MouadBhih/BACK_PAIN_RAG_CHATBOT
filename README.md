# 🧑‍⚕️ Back Pain RAG Chatbot

A medical Q&A chatbot focused on back pain, built with **Retrieval-Augmented Generation (RAG)**. It retrieves relevant passages from peer-reviewed research papers and generates doctor-style responses using a local LLM — no external APIs required.

---

##  Demo

> Ask questions like *"My lower back hurts. Should I rest in bed or keep moving?"* and get evidence-grounded, professional responses.

---

##  How It Works

```
User Question
     │
     ▼
Embed query (all-MiniLM-L6-v2)
     │
     ▼
FAISS vector search → Top-k relevant chunks from research PDFs
     │
     ▼
Build prompt (context + question)
     │
     ▼
Mistral-7B-Instruct generates doctor-style response
     │
     ▼
Gradio UI displays answer
```

---

##  Features

- **RAG pipeline** — grounds responses in actual medical literature, reducing hallucinations
- **Local LLM** — uses `mistralai/Mistral-7B-Instruct-v0.2` with no API calls
- **Medical safety guardrails** — the system prompt explicitly prevents diagnoses and medication prescriptions
- **Bilingual support** — designed to handle English and French queries
- **Gradio UI** — clean chat interface with public share link via Colab
- **PDF ingestion** — upload your own research papers at runtime

---

##  Project Structure

```
BACK_PAIN_RAG_CHATBOT.ipynb   # Main notebook (run top to bottom)
```

The pipeline inside the notebook:

| Step | Description |
|---|---|
| Install dependencies | `sentence-transformers`, `faiss-cpu`, `pypdf`, `transformers`, `gradio` |
| Upload PDFs | Interactive Colab upload widget |
| Parse & clean | Extract text, remove reference sections, filter short paragraphs |
| Chunk | Sliding window chunks (600 chars, 150 overlap) |
| Embed | `all-MiniLM-L6-v2` via `sentence-transformers` |
| Index | FAISS `IndexFlatL2` for similarity search |
| LLM | `Mistral-7B-Instruct-v0.2` in float16 |
| UI | Gradio `ChatInterface` with public share link |

---

##  Getting Started

### Run on Google Colab (recommended)

1. Open the notebook in [Google Colab](https://colab.research.google.com/)
2. Set the runtime to **GPU** (T4 or better) under *Runtime → Change runtime type*
3. Run all cells top to bottom
4. Upload your back pain research PDFs when prompted
5. Click the Gradio share link to open the chatbot

### Papers used in original demo

- Andersson, G.B.J. (1998). *Epidemiology of low back pain*. Acta Orthopaedica Scandinavica.
- *Nonspecific Low Back Pain* (clinical overview PDF)
- *The Epidemiology of Low Back Pain* (additional reference PDF)

You can replace or add any PDF on the topic.

---

##  Tech Stack

| Component | Library / Model |
|---|---|
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector store | `faiss-cpu` |
| PDF parsing | `pypdf` |
| LLM | `mistralai/Mistral-7B-Instruct-v0.2` |
| LLM framework | `transformers` + `accelerate` |
| UI | `gradio` |
| Runtime | Google Colab (TPU V5E / GPU) |

---

##  System Prompt & Safety

The LLM is instructed to behave as a medical assistant with strict guardrails:

```
- Do NOT diagnose diseases
- Do NOT prescribe medications
- Provide general medical advice only
- Use calm, professional language
- Mention warning signs (red flags) when relevant
```

---

##  Disclaimer

This chatbot is for **informational and educational purposes only**. It does not constitute medical advice, diagnosis, or treatment. Always consult a qualified healthcare professional for medical concerns.

---

## 📄 License

MIT
