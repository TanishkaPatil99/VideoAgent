# VideoAgent — Meeting Transcription & RAG Chat

Pipeline: YouTube/file → audio → transcript → summary → RAG-powered Q&A.

## Features

- **Audio Processing** — Extract audio from YouTube URLs or local video files via `yt-dlp` + `ffmpeg`
- **Transcription** — Speech-to-text using OpenAI Whisper (configurable model size)
- **Summarization** — Generate concise meeting summaries and titles via Mistral AI
- **Extraction** — Action items, key decisions, and open questions extracted automatically
- **RAG Chat** — Ask questions about the transcript using Chroma vector store + Mistral AI
- **Streamlit UI** — Dark-themed dashboard with live pipeline progress

## Setup

```bash
# Clone & enter
git clone https://github.com/TanishkaPatil99/VideoAgent.git
cd VideoAgent

# Create virtual environment
python -m venv .venv
.venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Environment variables (create .env)
MISTRAL_API_KEY=your_mistral_key
SARVAM_API_KEY=your_sarvam_key     # only needed for Hinglish transcription

# Run
streamlit run app.py
```

## Usage

1. Paste a YouTube URL or local file path in the sidebar
2. Select language (English / Hinglish)
3. Click **Analyse**
4. View summary, action items, decisions, and questions
5. Chat with the meeting transcript

## Tech Stack

| Component | Tool |
|-----------|------|
| UI | Streamlit |
| Transcription | OpenAI Whisper / Sarvam AI |
| LLM | Mistral AI (`mistral-small-latest`) |
| Embeddings | HuggingFace (`all-MiniLM-L6-v2`) |
| Vector Store | Chroma (LangChain) |
| Audio | yt-dlp + ffmpeg + pydub |

## Project Structure

```
VideoAgent/
├── app.py                     # Streamlit entry point
├── main.py                    # CLI entry point
├── core/
│   ├── transcriber.py         # Whisper / Sarvam transcription
│   ├── summarizer.py          # Title & summary generation
│   ├── extractor.py           # Action items, decisions, questions
│   ├── rag_engine.py          # RAG chain (retrieve + generate)
│   └── vector_store.py        # Chroma build / load / retriever
└── utils/
    └── audio_processor.py     # yt-dlp + ffmpeg audio extraction
```
