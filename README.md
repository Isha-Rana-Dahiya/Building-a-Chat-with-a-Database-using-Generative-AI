# Chat with Database using Generative AI  
Build a system where users can "chat" with a structured database using natural language queries, leveraging the powerful capabilities of Generative AI models. Unlike traditional database query methods, this approach allows retrieving and interacting with data in user-friendly ways without requiring technical knowledge of query languages like SQL.

Your customer has a structured relational database containing information relevant to their business. The goal is to create a system that allows users to interact with the database conversationally, extract insights, and manipulate data using natural language.

A conversational AI system is built leveraging on AI Stack **Azure AI Search, Azure SQL DB, Azure Open AI Service(GPT-4.1 model), and text-embedding-3-small model** 

## Features  

-  **Azure Open AI Service**  GPT 4.1 
-  **Structured Query Processing** using Azure SQL DB  
-  **azure AI Search** (basic tier) with semantic and vector embeddings 
-  **Azure AI Foundry Deployment**  text-embedding-3-small model


## Setup & Deployment  
1. **Provision Azure AI Search**  
   - Configure **vector index** with `text-embedding-3-small`.  
   - Enable **semantic ranker** for relevance.  

2. **Deploy Azure SQL Database**  
   - Upload structured dataset (`Dataset1.1.csv`).  
   - Define **query processing logic**.  

3. **Integrate GPT-4.1 for Query Understanding**  
   - Set up **Azure OpenAI API**.  
   - Enable **context-aware query refinement**.  

4. **Deploy via Azure AI Foundry**  
   - Use **Azure Portal** to manage resources.  
   - Monitor logs via **Azure Monitor**.  

## Usage  
Send a **query request** to:  
```bash
curl -X POST "https://your-deployment-url.com/query" -d '{"query": "Find me sunglasses under $50"}' -H "Content-Type: application/json"
