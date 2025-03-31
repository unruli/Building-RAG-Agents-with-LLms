# RAG Application with Nvidia-NIM

# 🤠 RAG Application with NVIDIA NIM + Streamlit

This project was to build a **Retrieval-Augmented Generation (RAG)** pipeline using **NVIDIA's NIM (NeMo Inference Microservices)** and **LangChain**, with a Streamlit UI for interaction. The project processes documents (PDFs), creates vector embeddings, and allows natural language querying over the content using powerful LLM capabilities.

---

## 🏛️ Key Technologies Used

- **NVIDIA NIM / NeMo**: For generating responses using `meta/llama3-70b-instruct` through `ChatNVIDIA` and `NVIDIAEmbeddings`
- **LangChain**: For managing document loading, splitting, embedding, and retrieval logic
- **Streamlit**: For building a simple user interface to interact with the RAG system
- **FAISS**: For creating a local vector store of embedded documents
- **Dotenv**: For loading environment variables securely

---

## 🚀 Core Components & Workflow

### 1. **Environment Setup**
- `.env` file stores the `NVIDIA_API_KEY`.
- Loaded into environment using `load_dotenv()`.

### 2. **Document Ingestion**
- Loads PDF documents from the `./us_census` folder using `PyPDFDirectoryLoader`.

### 3. **Text Chunking**
- Uses `RecursiveCharacterTextSplitter` to split long documents into smaller chunks of 700 characters with 50-character overlap.

### 4. **Vector Embedding**
- NVIDIA NIM's `NVIDIAEmbeddings` is used to embed document chunks.
- Embeddings are stored in an in-memory FAISS vector store.
- A button on the UI triggers this process (`Documents Embedding`).

### 5. **Retrieval-Augmented Generation (RAG)**
- When the user enters a question in the input box, a `ChatNVIDIA` model (`meta/llama3-70b-instruct`) is used to answer the question using:
  - A prompt template
  - A document retriever
  - A combined document + question answering chain (`create_stuff_documents_chain`)

### 6. **Display Results**
- The answer is displayed via `st.write()`.
- Relevant context chunks used to generate the answer are displayed under an expandable `Document Similarity Search` section.

---

## 📄 Usage Instructions

1. **Install Dependencies**:
   ```bash
   pip install streamlit langchain langchain-community langchain-core faiss-cpu python-dotenv
   ```

2. **Set Your NVIDIA API Key**:
   Create a `.env` file:
   ```bash
   NVIDIA_API_KEY=your_nvidia_api_key_here
   ```

3. **Run the App**:
   ```bash
   streamlit run app.py
   ```

4. **Workflow**:
   - Click the **"Documents Embedding"** button to preprocess and embed documents.
   - Ask a question about the documents using the text input field.
   - View the model's response and supporting document chunks.

---

## 🌐 Directory Structure

```
.
├── app.py
├── .env
├── us_census/              # Folder containing PDF documents
│   └── sample1.pdf
├── README.md
```

---

## 🔧 Future Improvements
- Add error handling and loading indicators
- Use persistent vector store (e.g., saved FAISS index)
- Upload documents via UI
- Model switching options

---

Built with ❤️ using NVIDIA NIM and LangChain.
