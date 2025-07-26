# 📚 Multilingual Retrieval-Augmented Generation (RAG) System

A simple, notebook-based system that allows users to upload a Bangla/English PDF, extract cleaned text using OCR, semantically embed it, and ask questions using a multilingual LLM-powered API (GROQ LLaMA 4).

---

## ⚙️ Setup Guide

> **Step 1:** Open the `.ipynb` notebook in **Google Colab**

> **Step 2:** Run all the cells **sequentially from top to bottom**. It will:
- Install dependencies
- Upload the PDF file
- Extract & clean OCR text
- Chunk and embed the data
- Start the FastAPI backend via ngrok
- Provide a terminal-based chatbot

> **Step 3:** At the **last cell**, interact with the system using multilingual queries (Bangla or English).

---

## 🧰 Used Tools, Libraries & Packages

| Library / Tool              | Purpose                                                                                     |
|----------------------------|---------------------------------------------------------------------------------------------|
| `pytesseract`              | OCR engine for extracting Bangla text from image-based PDFs                                  |
| `pdf2image`                | Converts PDF pages to images for OCR                                                        |
| `tesseract-ocr` & `tesseract-ocr-ben` | System-level OCR engine and Bangla language support                                   |
| `poppler-utils`            | Required backend for `pdf2image` to render PDFs                                            |
| `re` (built-in)            | Regular expression operations for cleaning noisy text                                      |
| `sentence-transformers`    | Converts text into dense vector embeddings for similarity matching                         |
| `chromadb`                 | Lightweight vector database for storing and querying embeddings                            |
| `transformers`             | Utilities and pipelines from HuggingFace's transformer models                              |
| `groq`                     | Python SDK to interact with the GROQ LLaMA 4 API                                          |
| `torch`                    | Backend used by transformers and sentence-transformers                                    |
| `shutil`, `os` (built-in) | File and system path handling                                                              |
| `typing` (built-in)        | Type hinting for better code clarity                                                      |
| `google.colab.files`       | Used for uploading files in Google Colab                                                  |
| `fastapi`                  | Web framework for serving the backend API                                                 |
| `uvicorn`                  | ASGI server for FastAPI                                                                   |
| `pyngrok`                  | Tunnel FastAPI to the internet using ngrok                                               |
| `nest_asyncio`             | Allows running asynchronous FastAPI inside Jupyter/Colab                                  |
| `threading`                | Used to run FastAPI server in background                                                  |
| `collections` (built-in)   | For managing short-term memory using `deque` and session state                            |
| `pydantic`                 | Data validation and settings management using models (`BaseModel`) in FastAPI             |


---

## 📋 Sample Queries and Outputs (Bangla & English)

![Screenshot 2025-07-26 191827](images/Screenshot%202025-07-26%20191827.png)
![Screenshot 2025-07-26 191845](images/Screenshot%202025-07-26%20191845.png)
![Screenshot 2025-07-26 191918](images/Screenshot%202025-07-26%20191918.png)
![Screenshot 2025-07-26 191933](images/Screenshot%202025-07-26%20191933.png)
![Screenshot 2025-07-26 191950](images/Screenshot%202025-07-26%20191950.png)

