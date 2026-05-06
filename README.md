# DigitalTwin

## Overview

DigitalTwin is an AI-powered web app that combines a React/Next.js frontend with a FastAPI backend to deliver a conversational "Digital Twin" experience. The backend stores session history as JSON files and uses the OpenAI API to generate assistant responses based on a custom personality prompt.

## Architecture

- `frontend/`
  - Next.js 16 app using React 19 and Tailwind CSS
  - Contains a chat UI and session management code
  - Sends user messages to the backend API at `http://localhost:8000/chat`
- `backend/`
  - FastAPI service exposing chat and health endpoints
  - Uses OpenAI via the `openai` Python SDK
  - Loads personality instructions from `backend/me.txt`
  - Persists conversation history under `memory/`

## Key Features

- Persistent chat sessions with session IDs
- Conversation memory stored as JSON files
- OpenAI-powered assistant with a custom Digital Twin personality
- Frontend built with modern Next.js and Tailwind styling

## Prerequisites

- Node.js 20+ and npm
- Python 3.13+
- OpenAI API key

## Setup

### Backend

1. Navigate to the backend folder:
   ```bash
   cd backend
   ```
2. Create and activate a virtual environment (recommended):
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Configure environment variables in `backend/.env`:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   CORS_ORIGINS=http://localhost:3000
   ```
5. Start the API server:
   ```bash
   uvicorn server:app --reload --host 0.0.0.0 --port 8000
   ```

### Frontend

1. Navigate to the frontend folder:
   ```bash
   cd frontend
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Start the development server:
   ```bash
   npm run dev
   ```
4. Open the app in your browser at `http://localhost:3000`

## Usage

- Type messages into the chat input.
- The frontend sends messages to the backend API.
- The backend forwards the chat history and current message to OpenAI.
- Session history is persisted in the `memory/` directory.
- The assistant acts as Ravi Kushwaha's Digital Twin, using the personality instructions from `backend/me.txt`.

## API Endpoints

- `GET /` — Basic API root response
- `GET /health` — Health check endpoint
- `POST /chat` — Send a message and receive an assistant reply
  - Request body:
    - `message` (string)
    - `session_id` (optional string)
- `GET /sessions` — List saved chat sessions with counts and last message details

## Environment Variables

- `OPENAI_API_KEY` — required to authenticate with OpenAI
- `CORS_ORIGINS` — allowed frontend origins for CORS (default: `http://localhost:3000`)

## Notes

- Conversation memory files are stored in `memory/` at the repository root.
- The assistant personality is defined in `backend/me.txt`.
- The frontend chat UI is implemented in `frontend/components/twin.tsx`.

## License

This repository does not include a license file. Add one if you plan to share or publish the project.
