# Gemini File Search

A powerful n8n workflow that enables intelligent document Q&A using Google Gemini's file search capabilities. Upload PDFs and query them using natural language to get accurate, source-cited answers.

## Overview

This workflow creates a complete RAG (Retrieval-Augmented Generation) system using Google Gemini's native file search feature. It allows you to upload documents, store them in a searchable file store, and interact with them through an AI agent that provides grounded, citation-backed responses.

![Gemini File Search Workflow](Gemini%20File%20Search.jpg)

## Architecture

The system consists of three main pipelines:

### Pipeline 1: File Store Creation
1. **Manual Trigger** - Initiates file store setup
2. **Create File Store** - Creates a Gemini file search store via API
3. **Store Configuration** - Sets up the storage location for documents

### Pipeline 2: Document Upload
1. **Form Submission** - Web form for file uploads
2. **Upload File** - Sends PDF to Gemini API
3. **Import File** - Adds uploaded file to the file search store

### Pipeline 3: Interactive Q&A
1. **Chat Interface** - Receives user queries via chat trigger
2. **RAG Agent** - Orchestrates the question-answering process
3. **Knowledge Base Tool** - Searches uploaded documents for relevant information
4. **Response Generation** - Uses Google Gemini to generate contextual, cited answers

### Pipeline 4: Evaluation (Optional)
1. **Dataset Trigger** - Loads test questions from Google Sheets
2. **Eval Agent** - Processes evaluation queries
3. **Evaluation Node** - Scores answer accuracy (1-5 scale)
4. **Metrics Storage** - Records results back to Google Sheets

## Components

### Data Sources
- **Form Trigger** - Web-based file upload interface
- **Google Sheets** - Evaluation dataset storage

### AI Services
- **Google Gemini API** - File search and chat capabilities
- **Gemini 2.5 Flash** - Language model for responses

### n8n Nodes
- Manual Trigger - Workflow initiation
- Form Trigger - File upload interface
- Chat Trigger - Interactive Q&A interface
- HTTP Request (multiple) - Gemini API interactions
- AI Agent - RAG orchestration
- HTTP Request Tool - Knowledge base queries
- Evaluation Trigger - Testing framework
- Evaluation Node - Answer quality assessment

## Setup

### Prerequisites
- n8n instance (self-hosted or cloud)
- Google Gemini API key
- Google Sheets API credentials (for evaluation)
- PDF documents for testing

### Configuration

1. **Get Your Gemini API Key**
   - Visit [Google AI Studio](https://aistudio.google.com/app/apikey)
   - Generate an API key
   - Add it to the HTTP Query Auth credentials in n8n

2. **Create File Store**
   - Click "Execute workflow" on the manual trigger
   - This creates a file search store in Gemini
   - Note the store name from the response (format: `fileSearchStores/xxxxx`)

3. **Update File Store References**
   - Open the "Import File" HTTP Request node
   - Replace the file store name in the URL with your store name
   - Open both "Knowledge Base" HTTP Request Tool nodes
   - Update the `file_search_store_names` value with your store name

4. **Configure Google Sheets (Optional - for evaluation)**
   - Set up Google Sheets OAuth2 credentials
   - Create a copy of the [sample evaluation dataset](https://docs.google.com/spreadsheets/d/1zf9jK8OdSrV4qMLwBjqrfML2tPx2SJmdqmxa4QN5TXU/copy)
   - Update the document ID in the evaluation nodes

5. **Upload Documents**
   - Access the form trigger webhook URL
   - Upload your PDF files (e.g., Apple 10-K, NVIDIA reports, Rules of Golf)
   - Wait for confirmation that files are imported

## Usage

### Uploading Documents
1. Navigate to the form trigger URL
2. Select a PDF file to upload
3. Submit the form
4. The workflow will:
   - Upload the file to Gemini
   - Import it into your file search store
   - Make it available for querying

### Chatting with Documents
1. Access the chat interface via the webhook URL
2. Ask questions about your uploaded documents
3. The RAG agent will:
   - Search the file store for relevant information
   - Generate accurate, grounded responses
   - Cite sources from your documents

### Running Evaluations
1. Prepare a Google Sheet with test questions and expected answers
2. Configure the evaluation trigger with your sheet
3. Execute the evaluation workflow
4. Review accuracy scores (1-5 scale) in the metrics output

## Sample Documents

The workflow includes three sample PDFs for testing:
- **Apple 10-K** - Apple's annual financial report
- **NVIDIA Annual Report** - NVIDIA's financial documentation
- **Rules of Golf Simplified** - Golf rules reference guide

## Features

- **Web-based file upload** with form interface
- **Native Gemini file search** for accurate retrieval
- **Interactive chat interface** for natural language queries
- **Source citation** in all responses
- **Automated evaluation framework** for quality testing
- **Multi-document support** for comprehensive knowledge bases
- **Grounded responses** to prevent hallucinations

## System Prompt

The RAG agent uses this system message:

```
You are a helpful RAG agent. Your job is to answer the user's question using your Knowledge Base tool to make sure all of your answers are grounded in truth. Please cite your sources when you're giving your answers.

When you are sending a query to the Knowledge Base tool, only send over text. No punctuation, quotation marks, or new lines.
```

## Evaluation Criteria

The evaluation system scores answers on a 1-5 scale:

- **5**: Highly similar - Nearly identical to ground truth
- **4**: Somewhat similar - Largely similar with few differences
- **3**: Moderately similar - Core essence captured with some differences
- **2**: Slightly similar - Few matching elements
- **1**: Not similar - Significantly different from ground truth

## API Endpoints

The workflow uses these Gemini API endpoints:

- **Create Store**: `POST https://generativelanguage.googleapis.com/v1beta/fileSearchStores`
- **Upload File**: `POST https://generativelanguage.googleapis.com/upload/v1beta/files`
- **Import File**: `POST https://generativelanguage.googleapis.com/v1beta/fileSearchStores/{store-id}:importFile`
- **Generate Content**: `POST https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash:generateContent`

## Workflow Tags
- AI AGENT
- RAG
- FILE SEARCH
- DOCUMENT Q&A

## Best Practices

1. **File Store Management**: Create one file store per knowledge domain
2. **Document Quality**: Use clear, well-formatted PDFs for best results
3. **Query Optimization**: Ask specific questions for more accurate answers
4. **Evaluation**: Regularly test with known questions to monitor quality
5. **Source Citation**: Always verify cited sources in responses

## Troubleshooting

**Files not uploading?**
- Verify Gemini API key is valid and has proper permissions
- Check that PDF files are not corrupted or password-protected
- Ensure file size is within Gemini's limits

**Queries returning empty results?**
- Confirm files were successfully imported to the file store
- Verify the file store name is correct in all nodes
- Check that the query is relevant to uploaded documents

**Evaluation not working?**
- Ensure Google Sheets credentials are configured
- Verify the sheet has columns: Input, Expected Answer
- Check that the document ID and sheet name are correct

## Credits

**Author:** [Nate Herk](https://www.youtube.com/@nateherk)

## Documentation

For additional information, refer to:
- Workflow diagram: `Gemini File Search.jpg`
- Workflow definition: `Gemini File Search.json`
- Sample documents: `Apple 10-k.pdf`, `NVIDIAAn (1).pdf`, `Rules_of_Golf_Simplified (1).pdf`

## License

This project is provided as-is for educational and development purposes.
