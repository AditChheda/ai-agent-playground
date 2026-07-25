# AI Agent Playground

A collection of small, self-contained AI agent projects; experiments in building agents with LLMs, tool use, and agentic workflows. Each project lives in its own numbered folder with its own dependencies, environment variables, and README.

## Projects

| # | Project | Description |
|---|---------|-------------|
| 01 | [linkedin-qa-agent](01-linkedin-qa-agent/) | A "digital twin" chatbot that answers questions about your career and background, built from a LinkedIn PDF export and a short bio. Uses Claude with tool calling to record visitor contact info and unanswered questions. |

More projects will be added here as they're built.

## Structure & conventions

- Each project is a numbered, kebab-case folder: `NN-project-name/` (e.g. `01-linkedin-qa-agent`).
- Every project is self-contained: its own `requirements.txt`, its own `.env` (gitignored, never committed), and its own `README.md` explaining what it does and how to run it.
- Projects are independent. There's no shared code between them. Copy what you need rather than adding cross-project dependencies.

## Getting started with a project

Each project has setup instructions in its own README.
