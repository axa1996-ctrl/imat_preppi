# APEX Coach — AI Training Program Generator

AI-powered strength training program builder. Input athlete profile → get a full periodized program with sets, reps, percentages, and coaching rationale. Built with FastAPI + Claude API.

## What it does

- Generates complete 12-week training programs for **Squat** and **Bench Press**
- Supports 5 periodization models: Block, DUP, Wave Loading, Wendler 5/3/1, Modified Conjugate
- Programs include exact kg, RPE targets, accessories, and phase-by-phase coaching rationale
- Full Program Builder page generates multi-day weekly splits across all muscle groups
- CSV export for every generated program

## Tech stack

- **Backend**: Python, FastAPI, Anthropic Claude API (claude-sonnet-4-5)
- **Frontend**: Vanilla HTML/CSS/JS
- **AI layer**: Structured prompting with a verified protocol knowledge base — LLM output constrained to evidence-based programming principles

## Setup

```bash
cd apex-coach
pip install -r requirements.txt

# Set your Anthropic API key (Windows PowerShell)
$env:ANTHROPIC_API_KEY="your_key_here"

# Mac/Linux
export ANTHROPIC_API_KEY=your_key_here

cd backend
uvicorn main:app --reload
```

Open in browser: http://localhost:8000

## Project structure

```
apex-coach/
├── backend/
│   └── main.py                      # FastAPI — routes, LLM calls, CSV export
├── frontend/
│   └── index.html                   # UI — athlete form, program view, full builder
├── protocols/
│   ├── squat_powerlifting.json      # Legacy protocol file
│   └── full_program_database.json  # Volume landmarks, exercise DB, split templates
└── requirements.txt
```

## Architecture

- **Protocols separated from code** — knowledge base lives in JSON, not hardcoded in prompts
- **LLM layer separated from logic** — prompts in `build_system_prompt()` / `build_user_prompt()`, independent of routing
- **Backend separated from frontend** — can be replaced with React or mobile frontend without touching the API

## Periodization models

| Model | Description |
|---|---|
| Block | Sequential mesocycles — accumulation → intensification → realization |
| DUP | Daily Undulating — strength, power, hypertrophy sessions within same week |
| Wave Loading | Randomized high-variability non-linear — RPE-based autoregulation |
| Wendler 5/3/1 | Sub-maximal training with AMRAP sets, Training Max = 90% 1RM |
| Modified Conjugate | Concurrent ME + DE sessions, constant variation to prevent accommodation |
