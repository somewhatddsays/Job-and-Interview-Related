# How to Build a basic RAG System

## What we are building?
A RAG system that:
* Turns documents into searchable vectors
* Finds information using semantic search
* Sends relevant context to the LLM
* Generates accurate answers from your data

## Flow

### STEP-1:
#### Install the Required Libraries

```requirements
pip install openai chromadb langchain tiktoken
```

**What these libraries do:**

| Libraries   | Description                              |
|:------------|:-----------------------------------------|
| `OpeanAi`   | Creates embeddings and generates answers |
| `ChromeDB`  | Stores document vectors for fast search  |
| `LangChain` | Helps load and process documents         |
| `Tiktoken`  | Handles token counting for the model     |

⚠️ **Don't forget**:<br>Set your **_OpenAi key_** as environment variable

### STEP-2:
#### Load you Documents

```python
from langchain.document_loaders import PyPDFLoader

loader = PyPDFLoader("docs.pdf")
documents = loader.load()
```

**What happens here:**
* Reads your PDF file
* Extracts all the text from each page
* Keeps useful metadata (like page numbers)

Now you have the raw text ready for processing.

### STEP-3
### Split Text into Chunks

```python
from langchain.text_splitter import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(
    chunk_size = 500,
    chunk_overlap = 75
)

chunks = splitter.split_documents(documents)
```

**Why do we split text?**
* LLM can't process very large documents at once
* Smaller pieces make search more accurate
* Overlap keeps important context between chunks

Now your document is broken into AI-friendly pieces

### STEP-4
#### Create Embeddings
Converts your text vectors (numbers) so AI can understand meaning.

```python
from openai import OpenAi
client = OpenAi()

def embed(text):
    response = client.embeddings.create(
        model = "text-embedding-3-large",
        input = text
    )
    return response.data[0].embedding
```

**What this step does?**
* Converts text into vector representations
* Captures the semantic meaning of the text
* Makes documents searchable using similarity

⚠️ **Important**:<br>Use the same embedding model for indexing and quering.

### STEP-5
#### Store Vectors in a Database

Converts your text into vectors (numbers) so AI can understand meaning.

```python
import chromadb

chroma = chromadb.Client()
collection =  chroma.create_collection("rag_docs")

collection.add(
    documents = [c.page_content for c in chunks],
    embeddings = [embed(c.page_content) for c in chunks],
    ids = [str(i) for i in range(len(chunks))]
)
```
**What happends here?**
* Each text chunk gets converted into a vector
* Vectors are stored in ChromaDB
* This allows fast semantic search

Now your data is indexed and ready for retrieval.

### STEP-7
#### Select the best Context

```python
# From 20 results, we pick only the top 5
# More results = better recall, but too much
# Context confuses the LLM - 5 is the sweet spot

top_chunks = results["documents"][0][:5]
context = "\n\n".join(top_chunks)
```

**What happens here?**
* Select the top 5 most relevant chunks
* Combine them into one context block
* This context will be sent to the LLM

Now the AI has relevant information to generate an answer

### STEP-8
#### Build the Prompt

```bigquery
prompt = f"""
Answer ONLY using the context below.
If the answer is not present, say "I don't know".

Context:
    {context}
    Question:
        {user_query}
        """
```

**What this step does?**
* Adds the retrieved context to the prompt
* Includes the user's question
* Instruct the model to use only the provided information

This helps the AI give accurate, grounded answers.


### STEP-9
#### Generate the Answer

```python
reponse = client.chat.completions.create(
    model = "gpt-40-mini",
    messages = [{"role": "user", "content": prompt}]
)

print(response.choices[0].message.content)
```

**What happens here?**
* Send the prompt (question + content) to the LLM
* The model reads the retrieved documents
* Generates an answer based on that context

Now the AI answering using your own data.


### STEP-6
#### Retrieve Relevant Chunks

```python
user_query = "How do I reset my password?"
query_embedding = embed(user_query)

# Fetch more results than needed so we can pick only the best ones in the next step

results = collection.query(
    query_embedding = [query_embedding],
    n_results = 20
)
```
**What happens here?**
* The user question is converted into a vector
* We fetch 20 result first to give ourselves a wider pool &mdash; then in Step-7 we narrow it down to the 5 most relevant chunks for the LLM.
* The Vector Database searches for similar chunks
* Returns the most relevant pieces of text.

Now we have the context needed to answer the question.


### Before you Deploy

#### To improve quality:
* Add reranking for better search results
* Use metadata filters to refine retrieval
* Log retrieved chunks for debugging
* Evaluate with **RAGS** to measure performance

This helps your RAG system perform better in production.


**ORIGINAL POSTER** &mdash; [pycode.hubb](https://www.instagram.com/pycode.hubb/)









