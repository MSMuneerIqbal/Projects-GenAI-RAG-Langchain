# RAG Implementation with Pinecone Vector Database and PDF Data

This notebook demonstrates a Retrieval-Augmented Generation (RAG) system using Langchain, Google Generative AI, Pinecone vector database, and PDF document. The system is designed to answer questions by retrieving relevant information from the PDF document and using a large language model (LLM) to generate a response.

## Key Concepts

1.  **Setup and Installation**:
    *   The notebook begins by installing necessary libraries using `pip`:
        *   `pinecone`: Pinecone vector database client.
        *   `langchain-pinecone`: Langchain integration for Pinecone.
        *   `langchain-google-genai`: Integration for Google Generative AI models.
        *   `langchain_community`: Contains community contributed integrations.
        *   `pypdf`: For handling PDF files.

2.  **Accessing Pinecone API Key**:
    *   The notebook retrieves the Pinecone API key using `google.colab.userdata`.
    *   It initializes the Pinecone client using this API key.

3.  **Creating a Pinecone Index**:
    *   A Pinecone index named `"online-rag-project"` is created with the following configurations:
        *   `dimension=768`: Dimension of the vectors to be stored, matching the output dimension of your embedding model.
        *   `metric="cosine"`: Cosine similarity metric for measuring vector distance.
        *   `spec=ServerlessSpec(...)`: Specifies the serverless configuration (AWS in us-east-1 region).
    *   The notebook then initializes the pinecone index using `pc.Index(index_name)`.

4.  **Accessing Gemini API Key and Embedding Model**:
    *   The Gemini API key is accessed via `google.colab.userdata`.
    *   A `GoogleGenerativeAIEmbeddings` model with embedding model (`models/embedding-001`) is initialized for generating vector embeddings.

5. **Generate Embedding for text**
    * The embedding model is used to generate embeddings for sample text "This is the RAG project"

6.  **Vector Store Initialization**:
    *   A `PineconeVectorStore` is created using the initialized Pinecone index and embedding model. This allows Langchain to interact with the Pinecone database.

7.  **Loading and Splitting PDF Documents**:
    *   A function `load_and_split_pdf` is defined to:
        *   Load a PDF document from the given path using `PyPDFLoader`.
        *   Split the PDF into text chunks using `RecursiveCharacterTextSplitter`.
            * `chunk_size`: Max length of each chunk.
            * `chunk_overlap`: Overlap between chunks.
        *   Return the document chunks for further processing.
     *  It handles `FileNotFoundError` and other loading related errors.
    *   The PDF file `/content/Generative AI Suggested Projects For Hackathon.pdf` is loaded and split.

8. **Store embedding into vector db**
    * The text chunks are converted to vectors using embedding model and are stored into the `PineconeVectorStore`.

9.  **Data Retrieval**:
    *   The notebook demonstrates three different methods for similarity searching in the Pinecone vector store.
    *   `vector_store.similarity_search_with_score`: Retrieves results along with their similarity scores.
    *   `vector_store.similarity_search`: Retrieves results using k value to limit the results returned.
    *    `vector_store.similarity_search_with_relevance_scores`: Returns list of document and relevance score.
    *  The results are printed in a readable format.

## How it Works

1.  **Data Loading and Preparation**: PDF document is loaded, and split into chunks
2.  **Embedding Generation**: Each text chunk is converted into a vector representation using the Google Embeddings API.
3.  **Vector Storage**: The text embeddings are stored in a Pinecone vector store for efficient semantic search.
4.  **Information Retrieval**: When a query is made, it is converted to a vector representation and relevant text chunks are retrieved from the vector store based on the similarity score.
5.  **Response Generation**: The retrieved context and the original question can be combined and passed to a LLM (not shown in this notebook) to generate a natural language response based on the provided context.

## Usage

1.  Ensure you have the required libraries installed.
2.  Obtain a Pinecone API key and a Google API key and set them as secrets in your colab environment using userdata.
3.  Upload your PDF document to the colab environment.
4.  Run the notebook cells sequentially.
5.  Adjust parameters like `chunk_size` and `chunk_overlap` as needed.
6.  Add LLM integration to complete the RAG pipeline.

This notebook provides a base for building a RAG system with Pinecone, Google's GenAI and a PDF document. You can further enhance it by integrating with other LLMs, improving prompt engineering, and adding more retrieval techniques.