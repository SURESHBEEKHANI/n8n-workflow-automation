# RAG AI Agent

A Retrieval-Augmented Generation (RAG) system built with n8n that enables intelligent document-based conversations using vector embeddings and AI chat capabilities.

## Overview

This project implements a complete RAG pipeline that ingests documents from Google Drive, processes them into vector embeddings, and provides an AI-powered chat interface that can answer questions based on the stored knowledge.

![RAG AI Agent Workflow](RAG%20AI%20Agent.png)

## Architecture

The system consists of two main pipelines:

### Pipeline 1: Data Ingestion
1. **Document Download** - Retrieves documents from Google Drive
2. **Text Processing** - Extracts and chunks text into manageable segments
3. **Embedding Generation** - Converts text chunks into vector embeddings using HuggingFace
4. **Vector Storage** - Stores embeddings in Pinecone vector database

### Pipeline 2: AI Chat Agent
1. **Chat Interface** - Receives user queries via chat trigger
2. **Context Retrieval** - Searches Pinecone for relevant document chunks (top 3 results)
3. **Response Generation** - Uses Google Gemini to generate contextual responses
4. **Memory Management** - Maintains conversation history for coherent interactions

## Components

### Data Sources
- **Google Drive** - Document storage and retrieval

### Vector Database
- **Pinecone** - Vector storage and similarity search (index: `rag`)

### AI Models
- **HuggingFace Inference** - Text embedding generation
- **Google Gemini (PaLM)** - Conversational AI and response generation

### n8n Nodes
- Manual Trigger - Initiates data ingestion workflow
- Chat Trigger - Handles incoming chat messages
- AI Agent - Orchestrates retrieval and generation
- Vector Store (Pinecone) - Manages embeddings
- Memory Buffer - Maintains conversation context

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google Drive API credentials
- Pinecone API key
- HuggingFace API token
- Google Gemini (PaLM) API key

### Configuration

1. **Import the workflow**
   - Import `RAG System/RAG AI Agent.json` into your n8n instance

2. **Configure credentials**
   - Google Drive OAuth2 API
   - Pinecone API
   - HuggingFace API
   - Google Gemini (PaLM) API

3. **Set up Pinecone index**
   - Create an index named `rag` in your Pinecone account
   - Configure dimensions based on your embedding model

4. **Configure document source**
   - Update the Google Drive file ID in the download node
   - Point to your knowledge base document

## Usage

### Ingesting Documents
1. Click "Execute workflow" on the manual trigger
2. The system will download, process, and store document embeddings
3. Wait for completion before querying

### Chatting with the Agent
1. Access the chat interface via the webhook URL
2. Ask questions related to your ingested documents
3. The agent retrieves relevant context and generates informed responses

## Features

- **Automated document processing** from Google Drive
- **Vector-based semantic search** for accurate context retrieval
- **Conversational memory** for multi-turn dialogues
- **Scalable embedding storage** with Pinecone
- **Flexible document loading** supporting various formats

## Workflow Tags
- AI AGENT
- RAG

## Documentation

For detailed setup instructions and credential configuration, refer to:
- `Setup-&-Credential-Document.pdf`
- Workflow diagram: `RAG AI Agent.png`

## License

This project is provided as-is for educational and development purposes.
