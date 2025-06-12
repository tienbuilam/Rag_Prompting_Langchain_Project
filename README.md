# RAG Application for Academic Question Answering

## Introduction

This project aims to develop a **Retrieval Augmented Generation (RAG)** application using the **LangChain** library. The primary goal is to answer academic questions by leveraging a curated collection of academic papers (in PDF format) as the knowledge source.

The core pipeline of this RAG application is designed as follows:

1.  **Document Ingestion and Vector Database Creation:**
    * Academic papers are processed by splitting them into smaller, manageable document chunks.
    * These chunks are then used to build a robust **Vector Database (VectorDB)** system, incorporating an efficient **embedding model** to convert text into numerical representations for similarity search.

2.  **Contextualized Querying:**
    * Upon receiving an input question, the system queries the VectorDB to retrieve text samples (documents) that are highly relevant to the question.
    * These retrieved samples serve as **context**, which is then dynamically incorporated into the prompt provided to the Large Language Model (LLM). This ensures the LLM has reliable, specific information to draw upon.

3.  **Answer Generation:**
    * The augmented prompt (containing both the user's question and the retrieved context) is fed into the LLM.
    * The LLM then generates a comprehensive and accurate answer based on the provided context, minimizing hallucinations and grounding its responses in the academic papers.

## Project Structure

The project's source code is organized within the `rag_langchain` directory, following a clear and modular structure to enhance maintainability and readability.

rag_langchain/  
├── data_source/  
│   ├── generative_ai/  
│   │  └── download.py  
├── src/  
│   ├── base/  
│   │   └── llm_model.py  
│   ├── rag/  
│   │   ├── file_loader.py  
│   │   ├── main.py  
│   │   ├── offline_rag.py  
│   │   ├── utils.py  
│   │   └── vectorstore.py  
│   └── app.py  
└── requirements.txt 


### Directory and File Descriptions:

* **`data_source/`**: This directory is dedicated to storing the academic papers that will be used to populate the VectorDB system.
    * **`data_source/generative_ai/download.py`**: Contains the script responsible for automatically downloading academic papers in PDF format from predefined sources.

* **`src/`**: This is the main directory for all application source code.
    * **`src/base/`**: Houses foundational components.
        * **`src/base/llm_model.py`**: Defines the function(s) for initializing and configuring the Large Language Model (LLM) used in the RAG pipeline.
    * **`src/rag/`**: Contains all modules specifically related to building and operating the RAG system.
        * **`src/rag/file_loader.py`**: Implements functions for loading and processing PDF documents, preparing them for text extraction and splitting.
        * **`src/rag/main.py`**: Orchestrates the RAG process, including the initialization of LangChain chains that connect the retrieval and generation phases.
        * **`src/rag/offline_rag.py`**: Manages the construction of the prompt template, integrating the user's question with the retrieved context before sending it to the LLM.
        * **`src/rag/utils.py`**: Provides utility functions, such as logic to parse and extract the final answer from the LLM's raw output.
        * **`src/rag/vectorstore.py`**: Contains the code for initializing and managing the VectorDB system, including the embedding model configuration.
    * **`src/app.py`**: The main application file, responsible for setting up and initializing the API endpoint for the RAG application.

* **`requirements.txt`**: Lists all necessary Python libraries and their versions required to run the project successfully, ensuring environment reproducibility.