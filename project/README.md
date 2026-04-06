# AI-Powered NL2SQL Chatbot (Vanna 2.0 + FastAPI)

## Project Description

This project is a Natural Language to SQL (NL2SQL) system built using Vanna AI 2.0, FastAPI, and SQLite.

It allows users to ask questions in plain English (e.g., "Top 5 patients by spending") and automatically:

Converts the question into SQL

Executes it on a database

Returns results with a summary and visualization

The system simulates a clinic management system with patients, doctors, appointments, treatments, and invoices.


# Tech Stack

Python 3.10+

Vanna AI 2.0

FastAPI

SQLite (built-in)

Plotly (for charts)

Pandas

LLM Provider: Google Gemini (gemini-2.5-flash)


# Project Structure

project
│

├── setup_database.py     # Creates DB + inserts dummy data


├── seed_memory.py        # Seeds agent memory with Q&A


├── vanna_setup.py        # Vanna 2.0 agent setup


├── main.py               # FastAPI app


├── requirements.txt      # Dependencies


├── README.md             # Documentation


├── RESULTS.md            # Test results


└── clinic.db             # SQLite database




# Setup Instructions (Step-by-Step)

1. Clone Repository

2. Create Virtual Environment

3. Install Dependencies
   
pip install -r requirements.txt


4. Setup Environment Variables
   
For Google Gemini:

GOOGLE_API_KEY= xyz


5. Create Database

python setup_database.py

Create clinic.db

Insert dummy data (patients, doctors, appointments, etc.)


6. Run Memory Seeding Script

This step:

Preloads the AI agent with 15+ correct Q&A SQL examples

Improves accuracy of SQL generation

7. Start the API Server

uvicorn main:app --port 8000 --reload

Server will run at: http://127.0.0.1:8000




# API Documentation


1. Chat Endpoint

POST /chat

Request

{
  "question": "Top 5 patients by total spending"
}

Response

{
  "message": "Here are the top 5 patients by total spending.",
  
  "sql_query": "SELECT p.first_name, p.last_name, SUM(i.total_amount) AS total_spending ...",
  
  "columns": ["first_name", "last_name", "total_spending"],
  
  "rows": [
  
    ["John", "Doe", 4500],
    
    ["Jane", "Smith", 3200]
    
  ],
  
  "row_count": 5,
  
  "chart": {
  
    "data": [...],
    
    "layout": {...}
    
  },
  
  "chart_type": "bar"
  
}


2. Health Check

GET /health


Response


{

  "status": "ok",

  "database": "connected",
  
  "agent_memory_items": 15
  
}


# Architecture Overview


User Question (Natural Language)

        ↓
        
FastAPI Backend (/chat endpoint)

        ↓
        
Vanna 2.0 Agent
  - LLM (Gemini)
  - ToolRegistry
  - Agent Memory
    
        ↓
    
SQL Generation

        ↓
        
SQL Validation (SELECT-only, safe queries)

        ↓
        
SQLite Execution (SqliteRunner)

        ↓
        
Results Processing (Pandas)

        ↓
        
Chart Generation (Plotly)

        ↓
        
JSON Response to User
