# AgriGPT â€” Multilingual Voice Assistant for Farmers

A RAG-based agriculture assistant that answers farming questions in four Indian languages through voice or text.

Built to be usable by people who are more comfortable speaking than typing: the user asks a question, the backend retrieves relevant agricultural material, and a large language model answers in the user's language.

## Architecture

```
React frontend  ->  FastAPI backend  ->  Retriever (RAG)  ->  Gemini 1.5 Flash
                          |                                        |
                    Google Translate  <---------------------------+
```

- **Retrieval**: `retriever.py` fetches relevant context from the curated `data/` corpus before generation, keeping answers grounded in agriculture material.
- **Generation**: Gemini 1.5 Flash through LangChain (`langchain-google-genai`).
- **Multilingual output**: `googletrans` translates the answer, so one knowledge base serves all supported languages.
- **Voice**: Whisper ASR converts speech to text on the client path; answers are played back as speech.
- **CORS**: restricted to the deployed Netlify origin.

## Stack

Python, FastAPI, LangChain, Gemini 1.5 Flash, Whisper, Google Translate, React, Tailwind CSS

## Run locally

```bash
git clone https://github.com/Vibhin-818/AgriAI.git
cd AgriAI
pip install -r requirements.txt
```

Create a `.env` file:

```
GOOGLE_API_KEY=your_key_here
```

```bash
uvicorn api:app --reload
```

Frontend lives in the `agriGPT3` / `agrigpt-web` repository and points at this API.

## Notes

- API keys are read from the environment; never commit `.env`.
- Retrieval runs before generation, so answers stay tied to the source corpus instead of relying on the model alone.
