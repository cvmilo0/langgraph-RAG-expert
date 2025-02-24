# LangGraph Expert 🤖

This project is an expert assistant for LangGraph that combines a web crawler for LangGraph documentation with an interactive Streamlit user interface.

## Main Features 🌟

- **Documentation Crawler**: Automatically crawls and processes official LangGraph documentation
- **RAG (Retrieval Augmented Generation)**: Uses embeddings and semantic search to provide accurate answers
- **Streamlit User Interface**: Intuitive chat interface to interact with the assistant
- **Asynchronous Processing**: Efficient implementation using asyncio for concurrent operations

## Requirements 📋

```
python >= 3.8
openai
supabase
streamlit
crawl4ai
pydantic
logfire
httpx
python-dotenv
```

## Setup 🔧

1. Create a `.env` file with the following variables:

```env
OPENAI_API_KEY=your_openai_api_key
SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_KEY=your_supabase_service_key
LLM_MODEL=gpt-4o-mini  # or your preferred model
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

## Usage 🚀

### Database Setup

Execute the SQL commands in `site_pages.sql` to set up your Supabase database:

1. Create the necessary tables
2. Enable vector similarity search with pgvector
3. Set up Row Level Security policies

In Supabase:
1. Go to the "SQL Editor" tab
2. Paste the contents of `site_pages.sql`
3. Click "Run"

The database schema includes:
```sql
CREATE TABLE site_pages (
    id bigserial primary key,
    url varchar not null,
    chunk_number integer not null,
    title varchar not null,
    summary varchar not null,
    content text not null,
    metadata jsonb not null default '{}'::jsonb,
    embedding vector(1536),
    created_at timestamp with time zone default timezone('utc'::text, now()) not null
);
```

### Documentation Crawler

To update the knowledge base with the latest documentation:

```bash
python crawl_langgraph_docs.py
```

This will:
- Fetch URLs from the LangGraph documentation sitemap
- Crawl each page and split into chunks
- Generate embeddings using OpenAI's text-embedding-3-small model
- Store the processed content in Supabase

#### Chunking Configuration

The crawler uses intelligent chunking with the following features:
- Default chunk size: 5000 characters
- Preserves code blocks integrity
- Respects paragraph boundaries
- Maintains sentence coherence

### User Interface

To start the chat interface:

```bash
streamlit run streamlit_ui.py
```     

## Project Structure 📁

```
langgraph-expert/
├── crawl_langgraph_docs.py  # Documentation crawler and processor
├── langgraph_expert.py      # Main assistant logic
├── streamlit_ui.py          # Web interface
├── site_pages.sql           # Database setup commands
├── graph.py                 # LangGraph workflow definition
├── requirements.txt         # Project dependencies
└── .env.example            # Environment variables template
```

### Component Details:
- `crawl_langgraph_docs.py`: Handles documentation crawling, chunking, and storage
- `langgraph_expert.py`: Implements the RAG agent and query processing
- `streamlit_ui.py`: Provides the chat interface and response streaming
- `graph.py`: Defines the LangGraph workflow and agent interactions
- `site_pages.sql`: Contains all database setup commands

## Technical Features 🔍

- Text processing in chunks for efficient handling of long documents
- Embeddings system for semantic search
- Supabase storage for efficient knowledge base management
- Response streaming for better user experience
- Persistent conversation state management

## Contributing 🤝

Contributions are welcome. Please open an issue to discuss major changes before creating a pull request.

## License 📄

MIT 
