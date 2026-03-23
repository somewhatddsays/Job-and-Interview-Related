# A Complete Guide to RAG Chunking

### 1. Why chunking Exists in RAG
RAG (Retrieval-Augmented Generation) works in three stages:
- **Chunk Documents**
- **Embed Chunks**
- **Retrieve top-k chunks &rarr; Send to LLM**

Chunking is the foundation of the entire system.

If chunking is wrong:
- Retrieval fails
- Hallucinations increase
- Context gets fragmented
- Token costs explode

You are not chunking text <br>
You are chunking **knowledge units.**

---

### 2.What is a Chunk Really is
A chunk is the smallest retrievable unit of meaning.

**Bad chunk**:
```aiignore
The transformer architechture was introduced in 2017. Attention allows the model to...
```
(cut mid-idea)
<br>

**Good chunk**:
```aiignore
What is the Transformer architechture? It was introduced in 2017 by Vaswani et al. and use....
```
(One complete thought)

---

### 3. Chunking Controls the RAG Failure Models

| Failure                | Root Cause                      |
|:-----------------------|:--------------------------------|
| `LLM makes things up`  | Missing Chunk                   |
| `Wrong answer`         | Chunk too small                 |
| `Vague Answer`         | Chunk too large                 |
| `High Cost`            | Over-long chunks                |
| `Low recalll`          | Chunk boundaries break meaning  |

Chunking is not preprocessing. <br>
It is **retrieval architecture**

---

### 4. Core Chunking Parameters
#### 4.1 Chunk Size

Measured in tokens or characters.

| Use Case           | Recommended Size |
|:-------------------|:-----------------|
| `FAQs`             | 200-400 tokens   |
| `Documentation`    | 400-800 tokens   |
| `Legal/ Contracts` | 800-1200 tokens  |
| `Code`             | 200-500 tokens   |

**Why?**
- Embeddings lose precision after ~800 tokens
- LLM context gets polluted with noise

#### 4.2 Overlap
Chunks must overlap so knowledge isn't cut.

**Example** with 20% overlap:

```yaml
Chunk 1: tokens 0-400
Chunk 2: tokens 320-720
Chunk 3: tokens 640-1040
```

**Overlap preserves**:
- Definitions
- Cross-sentence logic
- References

**Typical overlap**: `10-25%`

---

### 5. The 5 Real Chunking Strategies

Let's break down what actually works in production.

#### 5.1 Fixed-Size Chunking
Split by token count.

```yaml
Every 500 token &rarr; new chunk
```

**Pros**
- Fast
- Simple
- Works for uniform text

#### 5.2 Sentence-Based Chunking

Split by sentence boundaries

```yaml
Group sentences until token limit is hit
```
Much better than fixed size.

**Pros**
- Preserves grammar
- Less semantic damage

**Cons**
- Still breaks topic boundaries

#### 5.3 Semantic Chunking

This is where real RAG begins.

Chunks are split when topic changes.

**You use**:
- Sentence embeddings
- Cosine similarity
- Break where similarity drops

**Example**
```yaml
If similarity(sentence_i, sentence_i + 1) < threshold &rarr; new chunk
```

**This produces**
- Concept-aligned chunks
- Self-contained knowledge blocks

This is the default for high-quality RAG systems.


#### 5.4 Document-Structure Chunking
Split by:
- Headers
- Sections
- Paragraphs
- Bullet Points

**Example**:

```shell
## Installation
&rarr; One chunk

## Configuration
&rarr; One chunk

## API Reference
&rarr; Sub-chunks per endpoints
```

This is perfect for:
- Docs
- Wikis
- Policies
- Research papers

Always preserve heading inside chunks.

#### 5.5 Hybrid Chunking (Production Standard)
Best practice:
1. Split by document structure
2. Inside each solution, apply semantic chunking
3. Apply size limits + overlap

**This creates:**
* Logically coherent chunks
* Embedding-friendly size
* Retrieval-optimized knowledge blocks

---

### Chunk Metadata as Important Text
Every chunk should store:
```json
{
  "chunk_id": "doc1_sec3_p2",
  "document": "API_Guide.pdf",
  "section": "Authentication",
  "page": 12,
  "tokens": 480
}
```
**Why**
Because retrieval without metadata is blind.

Metadata enables:
- Filtering
- Source citation
- Page-level grounding
- Reranking

---

### 7. What Happens After Chunking

The real pipeline:

```shell
Raw docs
&rarr; Chunking
&rarr; Embedding each chunk
&rarr; Vector DB
&rarr; Query embedding
&rarr; Similarity search
&rarr; Top-k chunks
&rarr; Reranker (optional)
&rarr; LLM
```

> Bad Chunking = Garbage embeddings.

---

### Chunk Size vs. Retrieval Accuracy

Here's the tradeoff:

| Chunk Size   | Retrieval                  | LLM Quality        |
|:-------------|:---------------------------|:-------------------|
| `Too small`  | High recall, low precision | Fragmented answers |
| `Too large`  | Low recall                 | Irrelevant context |
| `Just Right` | High recall + precision    | Clean answers      |


The sweet spot is:
**300 &mdash; 800 tokens with semantic boundaries**

---

### 9. How Chunking Impacts Hallucinations

**LLMs hallucinate when**:
* Required fact is not in retrieved chunks
* Fact is split across chunks
* Chunk is too noisy

**Good chunking reduces hallucination more than**:
* Prompt engineering
* Temperature
* Model size

---
 
### 10. Special Chunking Cases

#### 10.1 Tables
Do NOT split rows across chunks. <br>
Store tables as:
- CSV-like text
- Or one chunk per table

#### 10.2 Code
Chunk by:
* Function
* Class
* File

Never chunk by token count for code.

#### 10.3 PDFs
Chunk by:
* Page &rarr; Section &rarr; Paragraph

Preserve page numbers in metadata.

---

### 11. How to Know if Your Chunking is Bad
**Ask your RAG system**:
* What is X?
* Where is X defined?
* How does X work?

**If answers are**:
* Vague
* Half-correct
* Missing details



**ORIGINAL POSTER** : [analytics_vidhya](https://www.instagram.com/analytics_vidhya/)