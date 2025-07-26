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


---

## 📡 API Documentation

This project includes a FastAPI-based REST API for querying the Multilingual Retrieval-Augmented Generation (RAG) system.

---

### API Endpoint

- **POST** `/ask`

  - **Description:** Accepts a user query and optional session ID to return an answer based on the knowledge base and recent conversation history.
  - **Request JSON Body:**
    ```json
    {
      "query": "Your question here",
      "session_id": "optional-session-id"
    }
    ```
  - **Response JSON:**
    ```json
    {
      "answer": "Generated answer",
      "session_id": "session-id",
      "history": [
        {
          "query": "Previous question",
          "answer": "Previous answer"
        }
      ]
    }
    ```

---

### Running the API

1. Run the FastAPI server cell. It will print a public ngrok URL.


2. Run the interactive chat cell to communicate with the API via command-line input.

---

### Notes

- Session IDs maintain short-term conversation history (last 3 exchanges).
- The API responds in the same language as the query.
- If the answer is not found in the knowledge base, the API replies with "I don't know" in the query language.



---


## ❓ Project Questions and Answers

### 1. What method or library did you use to extract the text, and why?  
I used **pytesseract** with **pdf2image** to convert PDF pages into images and then perform OCR (Optical Character Recognition) to extract text. This approach was chosen because many PDFs, especially scanned documents or complex layouts, do not have easily extractable selectable text. Using OCR ensures text extraction even from such PDFs.  
**Formatting challenges:** Yes, the extracted text required cleaning due to artifacts like page headers/footers, numbering, and formatting marks, which were removed using regular expressions.

### 2. What chunking strategy did you choose?  
I used **paragraph-based chunking** with a maximum word limit (e.g., 200 words) per chunk. Paragraph-based chunking preserves semantic coherence, which helps in semantic retrieval because paragraphs usually represent a meaningful unit of information.

### 3. What embedding model did you use? Why?  
I used the **"intfloat/multilingual-e5-base"** model from SentenceTransformers. This model supports multiple languages, including Bangla and English, and produces dense vector embeddings that effectively capture semantic meaning, allowing for meaningful cross-lingual similarity comparisons.

### 4. How are you comparing the query with your stored chunks? Why did you choose this similarity method and storage setup?  
I compute embeddings for all chunks and the query using the embedding model, then use **ChromaDB** to store and perform vector similarity search based on cosine similarity. ChromaDB efficiently indexes and retrieves nearest neighbors for fast semantic search, making it suitable for large-scale document retrieval.

### 5. How do you ensure that the question and the document chunks are compared meaningfully? What if the query is vague or missing context?  
Meaningful comparison is ensured by using a strong multilingual embedding model that encodes semantic relationships beyond just keywords. However, if the query is vague or lacks context, retrieval results may be less relevant. The system then defaults to stating "I don't know" to avoid misleading answers.

### 6. Do the results seem relevant? If not, what might improve them?  
Results are generally relevant for well-formed queries. Improvements could include:  
- Better chunking strategies (e.g., overlapping chunks or sentence-based chunking)  
- Using larger or fine-tuned embedding models for the specific domain  
- Expanding the document base with more comprehensive or cleaner data  
- Incorporating query expansion or reformulation techniques  

