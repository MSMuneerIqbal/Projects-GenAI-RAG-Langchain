# RAG Implementation with CSV Data for University FAQs

This notebook demonstrates a Retrieval-Augmented Generation (RAG) system using Langchain, Google Generative AI, and a CSV dataset of frequently asked questions (FAQs) for a university. The system is designed to answer questions by retrieving relevant information from the CSV file and using a large language model (LLM) to generate a response.

## Key Concepts

1.  **Setup and Installation**:
    *   The notebook begins by installing necessary libraries using `pip`:
        *   `langchain`: For building LLM-powered applications.
        *   `pinecone-client`: A vector database client (not directly used in this version, but often part of RAG implementations)
        *   `google-generativeai`: Google's Gemini API wrapper.
        *   `openai`: OpenAI API client (not used directly in this notebook).
        *   `tqdm`: For progress bars (not directly used).
        *   `chromadb`: For local vector store.
        *  `langchain-community` - contains community contributed integrations
         * `langchain-google-genai` - contains integration for google's genai models.

2.  **Import Necessary Libraries**:
    *   The notebook imports essential modules from the installed libraries:
        *   `ChatGoogleGenerativeAI`: To interface with Google's Gemini models for chat completions.
        *   `GoogleGenerativeAIEmbeddings`: To create text embeddings using Google's API.
        *   `create_retrieval_chain`: To create retrieval chains.
        *   `Chroma`: To use a local vector database for storing embeddings.
        *   `CSVLoader`: To load data from a CSV file.
        *   `PromptTemplate`: For creating reusable prompt templates.

3.  **Loading the Dataset**:
    *   The notebook loads a CSV file named `faq_bot_university.csv` using `CSVLoader`.
    *   The `source_column='Answer'` parameter specifies which column to use as source for the information.
    *   The loaded CSV data is stored in `documents`

4.  **Setting up API key**:
    * The API key is loaded using `google.colab` library.
    *  This step assumes that you have a `GOOGLE_API_KEY` stored in the colab secrets.

5.  **Text Splitting**:
    *   The `CharacterTextSplitter` is used to split the loaded documents into smaller chunks.
        *  `chunk_size=1000`: Specifies maximum length of the each chunk.
        *   `chunk_overlap=0`: Specifies no overlap between chunks.

6.  **Initializing Embeddings**:
    *   A `GoogleGenerativeAIEmbeddings` model is initialized, with a specified google api key and a text embedding model (`models/text-embedding-004`). This model is used to convert text into vector representations.

7.  **Creating a Vector Store**:
    *   A `Chroma` vector store is created from the split documents and embeddings.
     *  This vector store will hold the vectorized representation of text for semantic search.

8.  **Initializing LLM**:
     *  A `ChatGoogleGenerativeAI` model is initialized, using the specified google api key and a Gemini model (`gemini-1.5-flash`) for generating responses.

9. **Setting up retriever**
    *   The retriever is used to fetch the most relevant documents to the given prompt.
    *   The retriever is created using vector store with a `k` value of 5. This parameter controls how many relevant documents are returned by the retriever.

10. **Testing the retriever**:
    *  Here we are testing how our retriever is working
    *  we pass the prompt \"admission requirements\" to the retriever, and print the results

11. **Setting up Prompt Template and RAG Chain**:
    *  A `ChatPromptTemplate` is used to set up the system message and human message prompt.
    *  The system message defines the role of the chatbot and behavior.
    *  The human message asks the question using context and the user's question.
    * A `StrOutputParser` parses the output in string format.
    * A custom function `format_docs` is created to format the retrieved documents into string format.
    * The RAG chain is constructed by:
        *  Passing question along with the formatted context to the `chat_template`.
        *  Passing the `chat_template` to the llm
        *  Parsing the output using the `output_parser`

12. **Testing the RAG Chain**:
     *  A question is passed to the `rag_chain`.
     *  The response is printed on the console

13. **Setting up Retrieval QA chain**:
      *  `RetrievalQA` is another way of constructing rag chains.
      *  `RetrievalQA` is initialized with the llm and retriever.
      *  The chain_type parameter is set to `stuff`, which means the context will be stuffed into the prompt.

14. **Testing Retrieval QA Chain**:
      * A question is passed to the `faq_chain`.
      *  The response is printed on the console

## How it Works

1.  **Data Loading and Preparation**: The CSV data is loaded and split into smaller chunks.
2.  **Embedding Generation**: Each text chunk is converted into a vector representation using the Google Embeddings API.
3.  **Vector Storage**: The text embeddings are stored in a Chroma vector store for efficient semantic search.
4.  **Information Retrieval**: When a question is asked, the question is converted to a vector representation, and relevant text chunks are retrieved from the vector store.
5.  **Context Augmentation**: The retrieved context and the original question are combined and passed to the LLM.
6.  **Response Generation**: The LLM uses the augmented prompt to generate a natural language response based on the provided context.

## Usage

1.  Ensure you have the required libraries installed.
2.  Obtain a Google API key and set it as a secret in your colab using userdata
3.  Upload your CSV file named `faq_bot_university.csv` to the colab environment.
4.  Run the notebook cells sequentially.
5.  Modify or enhance the prompts and chain configurations to improve the response quality.

This notebook provides a basic template for building a RAG system using CSV data. You can expand on it by integrating with other vector databases, LLMs, and enhancing the prompt engineering.