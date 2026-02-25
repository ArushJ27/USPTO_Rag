# USPTO Patent Explorer

A RAG (Retrieval Augmented Generation) system for searching USPTO patent databases using natural language queries or technical drawings. Built with FAISS vector search, sentence-transformers, CLIP, and GPT-powered summaries.

## Features

- **Text Search** — Describe a patent in plain English and find the most relevant matches
- **Image Search** — Upload a technical drawing to find visually similar patents
- **AI Summaries** — GPT-generated summaries for search results and patent details
- **Interactive UI** — Gradio web interface with clickable patent previews

## Tech Stack

| Component | Technology |
|-----------|------------|
| Text Embeddings | `all-MiniLM-L6-v2` (sentence-transformers) |
| Image Embeddings | OpenAI CLIP (`clip-vit-base-patch32`) |
| Vector Search | FAISS |
| LLM Summaries | GPT via LiteLLM |
| Web Interface | Gradio |
| Data Processing | pandas, BeautifulSoup |

## Setup

```bash
pip install -r requirements.txt
```

Create a `.env` file with your OpenAI API key:

```
OPENAI_API_KEY=your_key_here
```

## Data Pipeline

Run these in order to process raw USPTO patent HTML files into searchable indices:

```bash
python code/parse_patents.py      # Extract patent metadata from HTML
python code/embed_text.py         # Generate text embeddings
python code/embed_image.py        # Generate image embeddings
python code/build_faiss.py        # Build FAISS index for images
```

## Usage

```bash
python code/app_gradio.py
```

Opens a local Gradio interface where you can search patents by text or image.

## Project Structure

```
code/
  app_gradio.py       - Main Gradio web application
  parse_patents.py    - Patent HTML parser
  embed_text.py       - Text embedding pipeline
  embed_image.py      - Image embedding pipeline
  build_faiss.py      - FAISS index builder
data/
  raw/                - Raw USPTO patent gazette HTML files
  processed/          - Extracted patent CSV data
embeddings/           - Pre-built FAISS indices and metadata
```
