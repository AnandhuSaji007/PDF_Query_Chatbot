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
- `chatbot.ipynb` → Jupyter notebook to run the chatbot.
- `requirements.txt` → Project dependencies.

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/AnandhuSaji007/PDF_Query_Chatbot
cd PDF-Query-Chatbo
```

### 2️⃣ Create a Virtual Environment
```bash
conda create -p venv python=3.12 -y
```

Activate it:
- **Windows**: `conda activate venv/`


### 3️⃣ Install Dependencies
```bash
pip install -r requirements.txt
```

### 4️⃣ Run the Agent
Open Jupyter Notebook and run:
```bash
chatbot.ipynb
```

## 📌 Author
Developed by **Anandhu Saji**
