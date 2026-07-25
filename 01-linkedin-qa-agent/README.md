# LinkedIn Q&A Agent

A conversational "digital twin" chatbot that answers questions about your career, background, skills, and experience. It is built from your LinkedIn profile and a short bio. Visitors can chat with it as if talking to you, and it will offer to record their contact details or flag questions it couldn't answer.

## How it works

1. **Context loading** ([context.py](context.py)) — extracts text from your `linkedin.pdf` export at startup and combines it with a short bio in `summary.txt` to build a system prompt that instructs the model to stay in character as your digital twin.
2. **Chat loop** ([app.py](app.py)) — a [Gradio](https://gradio.app) `ChatInterface` sends the conversation to Claude (Haiku 4.5) via the Anthropic API, using the OpenAI-compatible SDK client pointed at Anthropic's endpoint.
3. **Tool calls** ([tools.py](tools.py)) — the model can call two tools mid-conversation:
   - `record_user_details` — logs a visitor's email/name/notes when they want to be contacted.
   - `record_unknown_question` — logs any question the agent couldn't answer, instead of making up an answer.

   The agent loop in `app.py` keeps resubmitting to the model until it stops requesting tool calls, then returns the final reply.

## Setup

1. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
2. Create a `.env` file in this directory with your Anthropic API key:
   ```
   ANTHROPIC_API_KEY=your-key-here
   ```
3. Replace `linkedin.pdf` with your own LinkedIn profile export (PDF) and update `summary.txt` with a short bio about yourself.

## Running

```bash
python app.py
```

This launches a local Gradio web UI (with example prompts) where visitors can chat with your digital twin.

## Notes

- The tool functions in `tools.py` currently just print/return `"OK"`. Wire them up to an email service, CRM, or database if you want real notifications when a question goes unanswered or a visitor leaves their contact info.
- The model is set to `anthropic/claude-haiku-4.5` in [app.py](app.py); change `MODEL_NAME` to use a different Claude model.
