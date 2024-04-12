# Article Retrieval System

This project implements an advanced Article Retrieval System that utilizes FAISS for efficient similarity search and leverages the capabilities of GPT-3.5-turbo for generating insightful responses. The system is designed to process a collection of articles, index them for quick retrieval, and use a language model to generate answers to user queries based on the content of the retrieved articles.

## Dataset

The dataset comprises a comprehensive collection of blog posts sourced from Medium, specifically focusing on articles published under the "Towards Data Science" publication. The dataset is stored in a file named 'medium.csv', located in the project's root directory.

Dataset link: [1300 Towards Data Science Medium Articles Dataset](https://www.kaggle.com/datasets/meruvulikith/1300-towards-datascience-medium-articles-dataset)

## Configuration

1. **OpenAI API Key**: To use GPT-3.5-turbo, you need an API key from OpenAI:
   - Add your OpenAI API key to the `config.env` file as follows:
     ```
     OPENAI_API_KEY=your_api_key_here
     ```

2. **Data Preparation**: Place your article dataset CSV file in the project directory. The default filename expected is `medium.csv`, but you can use any name and adjust the `filename` variable in the notebook accordingly.

## Setup

1. Clone the repository:
   ```
   git clone https://github.com/werkah/rag-article-retrieval-system.git
   ```
2. Insert your OpenAI API key into the `config.env` file.
3. Use the default `medium.csv` dataset or upload your own and update the filename in the notebook accordingly.
4. Install the required dependencies at the beginning of the notebook:
```python
%pip install ydata-profiling langchain sentence_transformers faiss-cpu openai python-dotenv setuptools
```

## Usage

1. **Document Retrieval**:
To test document retrieval, define a query and call the `show_rag` function with it:
```python
query_text = "What is kNN?"
show_rag(query_text)
```

Customize the number of retrieved documents (k value) and the length of output text as needed in `show_rag` (default is k = 3 and output of length = 500)

2. **Response Generation**:
To see the output from the GPT-3.5-turbo model, define a query, create a retrieved_documents object, set the `max_tokens` size, and call `show_llm`:

```python
query_text = "What is kNN?"
retrieved_documents = retrieve_documents(query_text)
max_tokens = 150
show_llm(query=query_text, retrieved_documents=retrieved_documents, max_tokens = max_tokens, model="gpt-3.5-turbo")
```

## Features 

- Profile Report: Generates a comprehensive exploratory analysis report for the dataset using ydata-profiling.
- Document Loading and Splitting: Loads articles from the medium.csv file and processes them into manageable chunks.
- Document Retrieval: Demonstrates retrieving articles relevant to a sample query using FAISS.
- Interactive Querying: Allows users to enter their queries and see how the system retrieves relevant articles and generates responses.
- Response Generation: Utilizes GPT-3.5-turbo to generate contextually relevant answers based on retrieved information.

## Customization
- Token Limits: Adjust the `max_tokens` parameter in the response generation function to control the length of the responses from GPT-3.5-turbo.
- Dataset: Specify the dataset filename in the `filename` parameter.
- Embedding: Set the model name for embeddings in the `modelname` parameter. The default is `BAAI/bge-base-en-v1.5`.