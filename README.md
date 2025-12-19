# Compliancy Agent
Sample project exposing a product compliancy research capability to users.

## Components

### etl
Multi-steps process to fetch data from target website and transform it into a single structured nd-json file.
- extract : extracting and storing target website tables as heterogeneous set of json collections into a local data lake using puppeeter and rag calls to improve scraping precision
- transform : converting raw data from data lake into single structured nd-json file. 
- load : data ingestion step currently migrating the structured file to final database destination ( to be adapted depending on target database )

### api
Http server exposing inquiry capability to user through routes :
- POST /inquiries to submit a new inquiry
- GET /inquiries/:inquiryId to track the query state through a sse stream

### langgraph agent
Langgraph-based agent orchestrating the research, fetching results from product database and analyzing query compliancy against found records. 

### app 
React-based SPA exposing a free-text search to submit inquieries and tracking inquiry process by displaying the agent graph and messages until final result. 

## Architecture
![System architecture diagram](./architecture.png)