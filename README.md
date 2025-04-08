# GraphRAG: Knowledge Graph-Based Question Answering for United States Medical Licensing Examination Style Questions.

GraphRAG is an advanced question-answering system built specifically to reduce Large Language Models Hallucination. The system combines knowledge graph-based information and vector-based retrieval with large language models to provide comprehensive, evidence-based answers to complex medical questions.

## Overview

This project leverages Graph and Retrieval Augmented Generation (GraphRAG) to enhance medical Q&A by:

1. Processing USMLE-style medical questions
2. Retrieving relevant medical concepts from a knowledge graph (Neo4j)
3. Extracting textbook passages from a vector database (Pinecone)
4. Generating three types of answers for comparison:
   - LLM-Only Answer (Only LLM internal knowledge)
   - Context-Strict Answer (Only Knowledge Graph + Textbook Data)
   - LLM-Informed Answer (Combined Knowledge)
5. Evaluating answer quality and evidence-based reasoning

## Features

- **Knowledge Graph Integration**: Neo4j-based medical knowledge graph built from UMLS data
- **Vector Database**: Pinecone vector store for efficient retrieval of relevant textbook passages
- **Multi-Modal Answering**: Compare answers from different approaches to understand reasoning
- **Interactive UI**: Streamlit-based web interface for easy interaction
- **Comprehensive Evaluation**: Built-in metrics for answer quality and evidence assessment

## Prerequisites

- Python 3.9+
- Neo4j database (local or cloud instance)
- OpenAI API key
- Pinecone account and API key
- UMLS data files (for knowledge graph construction)
- Link:https://www.nlm.nih.gov/research/umls/index.html
- Medqa textbook dataset (for Vector store construction)
- Link:https://github.com/jind11/MedQA/tree/master?tab=readme-ov-file

## Installation

1. Clone the repository:
   ```
   git clone https://github.com/Tharun2331/GRAPHRAG.git
   cd GRAPHRAG
   ```

2. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

3. Set up environment variables by creating a `.env` file:
   ```
   OPENAI_API_KEY=your_openai_api_key
   NEO4J_URI=bolt://localhost:7687  # or your Neo4j instance URI
   NEO4J_USERNAME=neo4j
   NEO4J_PASSWORD=your_password
   PINECONE_API_KEY=your_pinecone_api_key
   PINECONE_ENV=your_pinecone_environment
   LANGSMITH_API_KEY=your_langsmith_api_key  # optional for tracing
   LANGSMITH_PROJECT=your_project_name  # optional
   ```

## Running the Application

### Web Interface

To run the interactive web interface:

```
cd GraphRag/scripts
streamlit run app.py
```

The web application will be accessible at http://localhost:8501 by default.

### Command Line Interface

For command-line operation:

```
cd GraphRag/scripts
python combined_usmle_2.py
Provide question below this message:
Enter your USMLE question (or command):
```

This will start an interactive session where you can enter USMLE-style questions and receive answers.

## Knowledge Graph Setup

If you need to build or update the knowledge graph from UMLS data:

```
cd GraphRag/scripts
python process_umls_embeddings.py --data_dir /path/to/umls/files --target_step ALL
```
If you need to build the vector store out of chunk from the textbook from medqa data:
 ```
 cd GraphRag/src/processors/
 python medqa_processor.py 
 ``` 

## Evaluation

To evaluate the system's performance on a set of USMLE questions:

```
cd GraphRag/scripts/
python combined_usmle_2.py
choose benchmark option
```

## Project Structure

- `GraphRag/scripts/` - Main application code
  - `app.py` - Streamlit web interface
  - `combined_usmle_2.py` - Core USMLE processor
  - `process_umls_embeddings.py` - Knowledge graph construction
  - `medqa_processor.py` - Vector database construction
- `GraphRag/tests/` - Testing and evaluation tools
- `requirements.txt` - Project dependencies

## Technologies Used

- **LangChain**: Framework for LLM application development
- **Neo4j**: Graph database for medical knowledge representation
- **OpenAI**: LLM provider for question understanding and answer generation
- **Pinecone**: Vector database for textbook passage retrieval
- **Streamlit**: Web interface framework
- **UMLS**: Unified Medical Language System for medical knowledge


## Acknowledgments

- UMLS for providing comprehensive medical terminology
- MedQA for providing comprehenisive medical textbooks
- OpenAI for LLM capabilities
- Neo4j and Pinecone for database technologies
