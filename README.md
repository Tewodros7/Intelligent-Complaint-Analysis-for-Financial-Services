# 🧠 Intelligent Complaint Analysis for Financial Services (RAG Chatbot)

This project is part of the **10 Academy KAIM 5 - Week 6** challenge. It aims to build a **RAG-powered internal chatbot** that allows teams at **CrediTrust Financial** to analyze thousands of customer complaints efficiently using **LLMs + semantic search**.

---

## 🧠 Business Context

**CrediTrust** receives thousands of monthly complaints about its financial products (credit cards, loans, BNPL, etc.). Product managers and compliance teams currently read complaints manually — costing time and losing insights.

We built a **Retrieval-Augmented Generation (RAG)** system to:
- Let users ask questions in natural language
- Retrieve relevant complaint narratives from a vector DB
- Generate grounded, actionable answers using a language model

---

## 🚀 Final Deliverables

- ✅ A cleaned & filtered CFPB complaints dataset
- ✅ Text embeddings chunked and stored in FAISS vector DB
- ✅ RAG core logic with evaluation
- ✅ Streamlit UI for interactive chat
- ✅ 📄 Final blog-style report

---

## 🧰 Tech Stack

| Component      | Tool/Library                        |
|----------------|-------------------------------------|
| Language Model | `sentence-transformers` (MiniLM)    |
| Vector DB      | `FAISS`                             |
| LLM Framework  | `LangChain`, `Transformers`, `Gemini`|
| UI             | `Streamlit`                         |
| Data           | CFPB Complaints Dataset             |
| Hardware       | GPU-enabled via PyTorch             |

---

## 📁 Project Structure

```bash
.
├── app/
│   ├── __init__.py
│   └── app.py                      # Streamlit app (Task 4)
│
├── src/
│   ├── README.md
│   └── rag_pipeline.py             # RAG core logic (Task 3)
│
├── data/
│   ├── complaints.csv
│   └── filtered_complaints.csv     # Cleaned dataset
│
├── vector_store/
│   ├── faiss_index.bin             # FAISS vector index
│   └── metadata.pkl                # Metadata for complaint chunks
│
├── notebooks/
│   ├── 0.1-eda.ipynb
│   ├── 2.0-embedding.ipynb
│   ├── 3.0-rag-agent.ipynb
│   ├── README.md
│   └── task_1_eda_and_preprocessing.ipynb
│
├── scripts/
│   ├── __init__.py
│   └── README.md
│
├── tests/
│   └── __init__.py
│
├── requirements.txt
├── .env                           # Contains GEMINI_API_KEY
└── README.md
```

---

## ✅ Task 1: EDA & Preprocessing

### 🔧 Actions:

* Loaded CFPB complaints CSV
* Filtered for 5 relevant products:

  * Credit card, Personal loan, Buy Now Pay Later (BNPL), Savings account, Money transfers
* Removed empty complaint narratives
* Cleaned text (lowercase, removed boilerplate)

### 📁 Output:

* `data/filtered_complaints.csv`

---

## ✅ Task 2: Chunking, Embedding & Indexing

### 🔧 Actions:

* Used `LangChain.RecursiveCharacterTextSplitter` with:

  * `chunk_size = 300`, `chunk_overlap = 50`
* Generated embeddings using:

  * `sentence-transformers/all-MiniLM-L6-v2` (on GPU)
* Stored embeddings + metadata using FAISS

### 📁 Output:

* `vector_store/faiss_index.bin`
* `vector_store/metadata.pkl`

---

## ✅ Task 3: RAG Pipeline + Evaluation

### 🔧 Actions:

* Implemented RAG logic in `rag_pipeline.py`:

  * Embed query → Search FAISS → Prompt Gemini with top-k chunks
* Prompt format:

  ```
  You are a financial analyst assistant for CrediTrust.
  Use the following context to answer:
  Context: {context}
  Question: {question}
  Answer:
  ```
* Evaluated the system using 5–10 sample queries

  * Metrics: answer relevance, groundedness, clarity

### 📁 Output:

* Evaluation table (Markdown)
* Analysis & tuning notes in final report

---

## ✅ Task 4: Interactive Chat Interface

### 🔧 Actions:

* Built an intuitive chat UI using **Streamlit**
* Users can:

  * Type questions in natural language
  * View LLM-powered answers
  * Expand and read the **retrieved complaint sources**
  * Clear conversation via sidebar
  * Enjoy a modern conversational layout

### 📸 Screenshots

#### 💬 Chat Starts

![Chat Start](assets/picture%20(2).png)

#### 🤖 Answer with Contextual Sources

![Answer with Sources](assets/picture_1.png)

#### 🧹 Sidebar with Clear Button

![Answer with Sources](assets/picture%20(1).png)

---

## 🧪 How to Run the App

### 1. Clone the Repository

```bash
git clone https://github.com/DagmMesfin/complaint-analysis-week6.git
cd complaint-analysis-week6
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set up your `.env` file

Create a `.env` file in the root directory and add:

```env
GEMINI_API_KEY=your_google_api_key_here
```

### 4. Launch the Streamlit Chat App

```bash
streamlit run app/app.py
```

Your browser should open to `http://localhost:8501` with the chat interface.

---
