# PDF-Query-Chatbot

This project is a **PDF Query Chatbot** that allows users to load PDF files, split them into chunks, embed the text using Hugging Face embeddings, store them in a Chroma vector database, and query the content using a Hugging Face LLM (Zephyr-7B).  

---

## 🚀 Features
- Load PDF documents using **PyPDFLoader**.
- Split text into manageable chunks with **RecursiveCharacterTextSplitter**.
- Generate embeddings with **HuggingFace Sentence Transformers**.
- Store and retrieve data from **ChromaDB**.
- Query PDFs using **Hugging Face LLMs** (Zephyr-7B).

---

## 📂 Project Structure
- `agentic.ipynb` → Jupyter notebook to run the chatbot.
- `requirements.txt` → Project dependencies.

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/your-username/PDF-Query-Chatbot.git
cd PDF-Query-Chatbot
```

### 2️⃣ Create a Virtual Environment
```bash
python -m venv agent
```

Activate it:
- **Windows**: `agent\Scripts\activate`
- **Linux/Mac**: `source agent/bin/activate`

### 3️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 4️⃣ Run the Agent
Open Jupyter Notebook and run:
```bash
jupyter notebook agentic.ipynb
```

---

## 🛠️ Code Overview

### 1. Load PDF
```python
loader = PyPDFLoader(file_path)
pages = []
async for page in loader.alazy_load():
    pages.append(page)
```

### 2. Split Text
```python
text_splitter = RecursiveCharacterTextSplitter(chunk_size=100, chunk_overlap=20)
texts = text_splitter.create_documents(raw_texts)
```

### 3. Embeddings + Vector Store
```python
embeddings_model = HuggingFaceEmbeddings(model_name="sentence-transformers/all-mpnet-base-v2")
db = Chroma.from_documents(texts, embeddings_model)
retriever = db.as_retriever()
```

### 4. LLM Integration
```python
llm_endpoint = HuggingFaceEndpoint(
    repo_id="HuggingFaceH4/zephyr-7b-beta",
    huggingfacehub_api_token=HF_TOKEN,
    task="text-generation",
    temperature=0.3,
    max_new_tokens=1024
)
llm = ChatHuggingFace(llm=llm_endpoint)
```

### 5. Define Chain & Query
```python
chain = (
    {"context": retriever, "query": RunnablePassthrough()}
    | prompt
    | llm
    | output_parser
)
print(chain.invoke("list the course outcomes"))
```

---

## 📌 Example Query
```text
User: list the course outcomes
Assistant: (Generates structured response using Zephyr-7B model)
```

---

## ✅ Next Steps
- Add multi-PDF support.
- Enhance query accuracy with RAG.
- Deploy chatbot as a web app (e.g., Streamlit/Gradio).

---

## 📌 Author
Developed by **Your Name**
