# AI Workflows Repository

A collection of n8n-based AI automation workflows for intelligent document processing and conversational AI systems.

## Workflows

### RAG AI Agent
A complete Retrieval-Augmented Generation (RAG) system that enables intelligent document-based conversations using vector embeddings and AI chat capabilities.

**Location:** `RAG System/`

**Key Features:**
- Automated document ingestion from Google Drive
- Vector-based semantic search with Pinecone
- AI-powered chat interface using Google Gemini
- Conversational memory for multi-turn dialogues
- HuggingFace embeddings for accurate retrieval

**Components:**
- Data ingestion pipeline (download → chunk → embed → store)
- AI chat agent with context retrieval
- Vector database integration (Pinecone)
- Multi-model AI architecture (HuggingFace + Google Gemini)

**Files:**
- `RAG AI Agent.json` - n8n workflow configuration
- `RAG AI Agent.png` - Visual workflow diagram
- `Setup-&-Credential-Document.pdf` - Detailed setup guide
- `README.md` - Complete documentation

[View RAG AI Agent Documentation →](RAG%20System/README.md)

## Getting Started

### Prerequisites
- n8n instance (self-hosted or cloud)
- API credentials for required services (varies by workflow)

### Installation
1. Clone this repository
2. Navigate to the desired workflow folder
3. Import the `.json` file into your n8n instance
4. Follow the workflow-specific README for setup instructions

## Project Structure

```
.
├── README.md                          # This file
└── RAG System/                        # RAG AI Agent workflow
    ├── RAG AI Agent.json              # Workflow definition
    ├── RAG AI Agent.png               # Workflow diagram
    ├── Setup-&-Credential-Document.pdf # Setup guide
    └── README.md                      # Workflow documentation
```

## Technologies

- **n8n** - Workflow automation platform
- **Pinecone** - Vector database
- **Google Gemini (PaLM)** - Large language model
- **HuggingFace** - Embedding models
- **Google Drive** - Document storage

## Contributing

Feel free to add new workflows or improve existing ones. Each workflow should include:
- n8n workflow JSON file
- Visual diagram (PNG/SVG)
- Comprehensive README
- Setup documentation

## License

This project is provided as-is for educational and development purposes.
