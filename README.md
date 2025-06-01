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
- Azure Open AI gets your data from Azure AI Search
- Intent Recognition: Azure AI Search use Azure AI Search index with Azure Open AI on your data.
- GPT-4.1 generates relevant SQL queries based on detected query patterns.
- Query Execution: The translated SQL runs on Azure SQL Database.
-	If semantic search is required, vector embeddings refine the query in Azure AI Search.
- Response Enhancement: GPT-4.1 summarizes retrieved data into a human-friendly response.
-	Additional filters or product recommendations may be suggested.

3. Inference: Generating a User-Friendly Response
-	Azure OpenAI GPT-4.1 refines the output.
-	Azure Open AI will answer our questions using Azure AI Search
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
   - import and vectorize data, in GPT 4.1, embeddings improve relevance. We need vector search for semantic similarity retrieval. It will enhance RAG.
   - create indexer, it automates index creation
   - create index, JSON file uploaded
   - datasource type Azure blob storage, is dataset stored as azure blob container, JSON file uploaded
   - skillsets set, JSON file uploaded
   - Configure **vector index** with `text-embedding-3-small`.  
   - Enable **semantic ranker** for relevance.
     ![image](https://github.com/user-attachments/assets/d90dd0fd-4377-4ce9-bfdb-39790d4e266a)
![image](https://github.com/user-attachments/assets/9d98691d-0d97-4b45-a6f3-6bf8523a7eba)

3. **Deploy Azure SQL Database**
   - Create Azure SQL DB resource, JSON file uploaded
   - Upload structured dataset (`Dataset1.1.csv`).  
   - Define **query processing logic**.

4. **Deploy Azure Storage Account**
   - Create Azure Storage account resource, JSON file uploaded
   - In data storage, create a container storing Dataset with blob type block blob   

5. **Deploy GPT-4.1 for Query Understanding**  
   - Create Azure OpenAI resource  
   - Go to Azure AI Foundry
   - Deploy GPT 4.1, customize token setting by reducing it to 30 requests per minute
     ![image](https://github.com/user-attachments/assets/97c96d24-b0a1-43c2-add2-d7d355e9a1b7)
- adding a datasource through blob storage
  ![image](https://github.com/user-attachments/assets/da8f0ebe-2509-4504-af68-79060b0deee0)
![image](https://github.com/user-attachments/assets/a9723c87-41eb-4e80-86df-e7bd173ee872)
![image](https://github.com/user-attachments/assets/54cdd44f-b49c-4a55-9659-087e9df6dd0f)

  Keep API key for data connection.

6. **Deploy embedding model text-embedding-3-small from model catalog via Azure AI Foundry**  
   - Use **Azure Portal** to manage resources.
   - Reduce the token limit for model to reduce cost.
   - Monitor logs via **Azure Monitor**.
   - If cost optimization is priority, text-embedding-3-small is the better choice. For higher precision for complex NLP tasks, text-embedding-3-large may be considered. I 
     considered cost optimization.

7. **Using AI Responsibly**
   - for deployment of models, under Gaurdrails and controls, we can filter the content.
     ![image](https://github.com/user-attachments/assets/82209bbd-5fb8-4bad-ba0e-fc36e5eee781)
     
8. **Interacting in Chat playground**
![image](https://github.com/user-attachments/assets/9ddd1959-69d7-4360-84bf-8f36f19e77c3)
![image](https://github.com/user-attachments/assets/8ea4c422-3172-4cbf-af53-0cc39fead718)
![image](https://github.com/user-attachments/assets/99021e51-286e-41ae-b263-bd8d7b8e1af2)
![image](https://github.com/user-attachments/assets/2d935083-746e-4802-96ea-46d4e5509f4f)

   

## Usage  
Send a **query request** to chat playground 
```bash
curl -X POST "https://your-deployment-url.com/query" -d '{"query": "Find me sunglasses under $50"}' -H "Content-Type: application/json"
