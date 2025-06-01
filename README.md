# Building-a-Chat-with-a-Database-using-Generative-AI
# Chat with Database using Generative AI  
A conversational AI system leveraging **Azure AI Search, Azure SQL DB, GPT-4.1, and text-embedding-3-small** for natural language querying.

## Features  

-  **Azure AI Foundry Deployment**  GPT 4.1
-  **Structured Query Processing** using Azure SQL DB  
-  **azure AI Search** with semantic and vector embeddings 
-  **Azure AI Foundry Deployment**  text-embedding-3-small


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
