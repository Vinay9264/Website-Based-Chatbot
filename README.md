# Website Q&A Chatbot Using Langchain and Groq

## Project Overview
This project is a Website Question–Answering Chatbot that allows users to ask questions about the content of a given website.
Instead of relying on general knowledge, the chatbot answers strictly based on the information available on the provided website.

The system follows a Retrieval-Augmented Generation (RAG) approach:
-> Website content is extracted and cleaned
-> Converted into vector embeddings
-> Stored in a vector database
-> Relevant content is retrieved for each user query
-> A Large Language Model generates an answer only using the retrieved content

The application is built using Streamlit for the interface and LangChain for orchestrating the RAG pipeline.


## Architecture Explanation

The project follows the below workflow:
### 1. User Input
-> User provides groq api key and then a website URL
-> User enters questions through a chat interface

### 2. Website Content Loading
-> Website data is fetched using a URL loader
-> Raw HTML content is extracted

### 3.Content Cleaning
-> HTML elements such as headers, footers, navigation bars, scripts, and styles are removed
-> Only meaningful textual content is retained

### 4.Text Chunking
-> Cleaned text is split into smaller overlapping chunks
-> This helps preserve context and improves retrieval accuracy

### 5.Embedding Generation
-> Each text chunk is converted into a numerical vector using a sentence embedding model

### 6.Vector Storage
-> All embeddings are stored in a FAISS vector database
-> The database is persisted locally for reuse

### 7.Question Answering
-> User queries are converted into embeddings

-> Most relevant chunks are retrieved from FAISS

-> Retrieved context is passed to the LLM

-> The LLM generates a response strictly from the provided context

### 8.Conversation Handling
-> Chat history is maintained to support follow-up questions


## Frameworks Used
### LangChain
-> LangChain is used to:

-> Load website documents

-> Split text into chunks

-> Generate embeddings

-> Build the conversational retrieval pipeline

-> Manage prompt templates and chat history

LangChain helps modularize the entire RAG workflow and makes the system easier to maintain and extend.


## LLM Model Used and Reason

Groq-hosted LLM (LLaMA / Mixtral family)
The Groq platform is used to access fast inference LLMs.
Reasons for choosing Groq:
-> Low latency response times

-> Reliable performance for retrieval-based tasks

-> Easy integration with LangChain

The model temperature is set to 0 to ensure:
-> Deterministic responses

-> Reduced hallucination

-> Consistent answers during evaluation


## Vector Database Used and Reason
### FAISS (Facebook AI Similarity Search)

FAISS is used as the vector database to store and retrieve embeddings.
Reasons for choosing FAISS:

-> Lightweight and fast

-> Ideal for local development

-> No external service dependency

-> Easy persistence and reload functionality

FAISS allows efficient similarity search, which is critical for retrieving relevant website content during question answering.


## Embedding Strategy

The project uses HuggingFace sentence embeddings
Model: sentence-transformers/all-MiniLM-L6-v2

### Embedding strategy details:

-> Website text is split into chunks of fixed size

-> Overlapping chunks are used to avoid loss of context

-> Each chunk is embedded independently

-> Embeddings are stored in FAISS for semantic search

This approach balances accuracy, speed, and memory usage.


## Setup and Run Instructions

1. Open the link in web browser : https://website-based-chatbot-wnwy5enhjjudkappx8qi993.streamlit.app/
2. Enter the Groq Api key
3. Enter the website url from which you want ask questions
4. Click in "Index Website Button"
5. Ask questions regarding the content of the website


## Assumptions

-> The website content is publicly accessible

-> The website contains meaningful textual data

-> The chatbot is expected to answer only from the provided website

-> Internet access is available during execution


## Limitations

-> Only single-page URLs are supported

-> Does not crawl multiple internal links

-> Performance depends on website structure and content quality

-> Images, videos, and dynamic content are not processed

-> Answers are limited strictly to extracted text


## Future Improvements

-> Multi-page website crawling

-> Support for PDF and document uploads

-> Better source citation for answers

-> Improved UI with highlighted references
-> Advanced memory handling for longer conversations
-> Deployment on cloud platforms
