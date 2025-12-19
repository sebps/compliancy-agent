# Compliancy Agent
Sample project exposing a product compliancy research capability to users.

## Installation
Command to checkout the whole project with submodules
`git clone --recurse-submodules git@github.com:sebps/compliancy-agent.git`

## Usage
1. etl — download data
- cd ./compliancy-agent-etl
- Open and follow the README.md instructions to install dependencies and run the extract/transform/load steps so the nd-json output is produced in the project data location.

2. api — spin up API server
- cd ./compliancy-agent-api
- Open and follow the README.md instructions to install dependencies, configure any required env vars and DB connections, and start the HTTP server.

3. app — start the interface
- cd ./compliancy-agent-app
- Open and follow the README.md instructions to install dependencies and run the React SPA. Open the displayed URL in a browser and submit queries that target the running API.

Notes:
- Ensure the API is configured to read the ETL output (or the database populated by ETL) before starting the app.
- Follow module READMEs in order (etl → api → app) to ensure data, server and UI are available.
- Total llm consumption from ETL component should not exceed $0.50 using Deepseek and default website target at https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=CELEX:02009R1223-20190813   

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

### agent
Langgraph-based agent orchestrating the research, fetching results from product database and analyzing query compliancy against found records. 

### app 
React-based SPA exposing a free-text search to submit inquieries and tracking inquiry process by displaying the agent graph and messages until final result. 

## Architecture
![System architecture diagram](./architecture.png)