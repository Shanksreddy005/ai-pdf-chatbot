# AI PDF Chatbot & Agent — Powered by LangChain and LangGraph

[![Next.js](https://img.shields.io/badge/Next.js-13-black?logo=next.js)](https://nextjs.org/)
[![LangChain](https://img.shields.io/badge/LangChain-v0.1-blue)](https://www.langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-Orchestration-brightgreen)](https://www.langchain.com/langgraph)
[![Supabase](https://img.shields.io/badge/Supabase-Vector_Store-3FCF8E?logo=supabase)](https://supabase.com/)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?logo=openai)](https://platform.openai.com/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> 💬 **Chat with your PDFs** — Upload documents, store embeddings in a vector DB, and ask natural language questions powered by LangChain, LangGraph, and OpenAI.

---

## 📸 Preview

**Chatbot UI**  
![Chatbot Screenshot](https://github.com/user-attachments/assets/3a9ddea7-b718-476b-bdae-38839be20c12)

---

## 🚀 Features

- **PDF Ingestion Pipeline**  
  - Parses PDFs into `Document` objects  
  - Stores vector embeddings in **Supabase** for semantic search  

- **Retrieval Graph**  
  - Handles user questions  
  - Retrieves relevant document chunks  
  - Generates **concise, referenced answers**  

- **Real-Time Streaming**  
  - Partial responses stream from backend to frontend  

- **LangGraph Orchestration**  
  - State-machine-based ingestion & retrieval workflows  
  - Visual workflow debugging in LangGraph Studio  

- **Next.js Frontend**  
  - File upload UI  
  - Chat interface with “View Sources”  

---

## 🏗 Architecture Overview

```ascii
┌─────────────────────┐    1. Upload PDFs    ┌───────────────────────────┐
│Frontend (Next.js)   │ ────────────────────> │Backend (LangGraph)       │
│ - React chat UI     │                      │ - Ingestion Graph         │
│ - File uploads      │ <────────────────────┤   + Supabase VectorStore  │
└─────────────────────┘    2. Confirmation   │                           │

┌─────────────────────┐    3. Ask questions  ┌───────────────────────────┐
│Frontend (Next.js)   │ ────────────────────> │Backend (LangGraph)       │
│ - SSE response      │                      │ - Retrieval Graph         │
│ - Show sources      │ <────────────────────┤   + LLM (OpenAI)          │
└─────────────────────┘ 4. Streamed answers  └───────────────────────────┘


- **Supabase** is used as the vector store to store and retrieve relevant documents at query time.  
- **OpenAI** (or other LLM providers) is used for language modeling.  
- **LangGraph** orchestrates the "graph" steps for ingestion, routing, and generating responses.  
- **Next.js** (React) powers the user interface for uploading PDFs and real-time chat.

The system consists of:
- **Backend**: A Node.js/TypeScript service that contains LangGraph agent "graphs" for:
  - **Ingestion** (`src/ingestion_graph.ts`) - handles indexing/ingesting documents
  - **Retrieval** (`src/retrieval_graph.ts`) - question-answering over the ingested documents
  - **Configuration** (`src/shared/configuration.ts`) - handles configuration for the backend api including model providers and vector stores
- **Frontend**: A Next.js/React app that provides a web UI for users to upload PDFs and chat with the AI.
---

