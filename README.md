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

### Documentation Crawler

To update the knowledge base with the latest documentation:

```bash
python crawl_langgraph_docs.py
```

### User Interface

To start the chat interface:

```bash
streamlit run streamlit_ui.py
```

## Project Structure 📁

- `crawl_langgraph_docs.py`: Crawler for LangGraph documentation
- `streamlit_ui.py`: Streamlit user interface
- `langgraph_expert.py`: Main assistant logic

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