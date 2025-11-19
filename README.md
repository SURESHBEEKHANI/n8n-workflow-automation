# AI Workflows Repository

A collection of n8n-based AI automation workflows for intelligent document processing and conversational AI systems.

## Workflows

### Automated Invoice Reminder System
An intelligent workflow that automatically sends payment reminders to customers based on invoice status, helping businesses maintain healthy cash flow and reduce manual follow-up work.

[View Documentation →](Automated%20Invoice%20Reminder%20System/README.md)

---

### RAG AI Agent
A complete Retrieval-Augmented Generation (RAG) system that enables intelligent document-based conversations using vector embeddings and AI chat capabilities.

[View Documentation →](RAG%20System/README.md)

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
├── README.md                                      # This file
├── Automated Invoice Reminder System/             # Invoice automation workflow
│   ├── Automated Invoice Reminder System.json     # Workflow definition
│   ├── Automated Invoice Reminder System.png      # Workflow diagram
│   └── README.md                                  # Workflow documentation
└── RAG System/                                    # RAG AI Agent workflow
    ├── RAG AI Agent.json                          # Workflow definition
    ├── RAG AI Agent.png                           # Workflow diagram
    ├── Setup-&-Credential-Document.pdf            # Setup guide
    └── README.md                                  # Workflow documentation
```

## Technologies

- **n8n** - Workflow automation platform
- **Google Sheets** - Data storage and management
- **Gmail** - Email delivery service
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
