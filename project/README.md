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

project/
│
├── setup_database.py     # Creates DB + inserts dummy data
├── seed_memory.py        # Seeds agent memory with Q&A
├── vanna_setup.py        # Vanna 2.0 agent setup
├── main.py               # FastAPI app
├── requirements.txt      # Dependencies
├── README.md             # Documentation
├── RESULTS.md            # Test results
└── clinic.db             # SQLite database
