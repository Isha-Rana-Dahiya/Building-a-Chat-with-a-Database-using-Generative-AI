# Chat with Database using Generative AI  
Build a system where users can "chat" with a structured database using natural language queries, leveraging the powerful capabilities of Generative AI models. Unlike traditional database query methods, this approach allows retrieving and interacting with data in user-friendly ways without requiring technical knowledge of query languages like SQL.

Your customer has a structured relational database containing information relevant to their business. The goal is to create a system that allows users to interact with the database conversationally, extract insights, and manipulate data using natural language.

A conversational AI system is built leveraging on AI Stack **Azure AI Search, Azure SQL DB, Azure Open AI Service(GPT-4.1 model), and text-embedding-3-small model** 

## Features  

-  **Azure Open AI Service**  GPT 4.1 
-  **Structured Query Processing** using Azure SQL DB  
-  **azure AI Search** (basic tier) with semantic and vector embeddings 
-  **Azure AI Foundry Deployment**  text-embedding-3-small model

## Flow Representations
1. Ingest: Structured Data Preparation
- Dataset Source: Your structured dataset (e.g., product catalog, sales transactions) is stored in Azure SQL Database.
- Data Processing: If using unstructured metadata (e.g., descriptions), it undergoes chunking and embedding via Azure AI Search.
- Structured tabular data is indexed using Azure SQL Indexer.

2. Develop: Natural Language Query Interface
- User Queries: Customers enter natural language questions such as "Suggest a brand for Rounded rectangular cat-eye reading glasses"
- Intent Recognition: Azure AI Search use Azure AI Search index with Azure Open AI on your data.
- GPT-4.1 generates relevant SQL queries based on detected query patterns.
- Query Execution: The translated SQL runs on Azure SQL Database.
-	If semantic search is required, vector embeddings refine the query in Azure AI Search.
- Response Enhancement: GPT-4.1 summarizes retrieved data into a human-friendly response.
-	Additional filters or product recommendations may be suggested.

3. Inference: Generating a User-Friendly Response
-	Azure OpenAI GPT-4.1 refines the output.
-	Give brand name and give details about glass feature.
-	Provides explanations (e.g., why certain brands are recommended).
-	Generates alternative query suggestions.
-	Results are sent to the user via chatbot UI, with formatted responses.
-	For Optimization, GPT-4.1 retains previous conversation context, refining responses dynamically.
- Uses multi-turn reasoning to provide clarifications, refinements, and detailed insights.
- Implements token optimizations, reducing unnecessary API calls
- Azure AI Search embeddings (text-embedding-3-small) to enhance search accuracy.
- For Secure handling:	Azure Key Vault for API Security for secure handling in GPT 4.1 secures API keys and database credentials
-	Response filtering prevents irrelevant results
-	Performance tuning enhances search responsiveness

## Setup & Deployment  
1. **Provision Azure AI Search**
   - create resource in basic tier
   - import and vectorize data
   - create index, JSON file uploaded
   - Configure **vector index** with `text-embedding-3-small`.  
   - Enable **semantic ranker** for relevance.  

3. **Deploy Azure SQL Database**  
   - Upload structured dataset (`Dataset1.1.csv`).  
   - Define **query processing logic**.  

4. **Integrate GPT-4.1 for Query Understanding**  
   - Set up **Azure OpenAI API**.  
   - Enable **context-aware query refinement**.  

5. **Deploy via Azure AI Foundry**  
   - Use **Azure Portal** to manage resources.  
   - Monitor logs via **Azure Monitor**.  

## Usage  
Send a **query request** to:  
```bash
curl -X POST "https://your-deployment-url.com/query" -d '{"query": "Find me sunglasses under $50"}' -H "Content-Type: application/json"
