# ECAM EPMI AI Webchat Assistant

**Stack** : Voiceflow · OpenAI GPT-4o · OpenAI GPT-3.5-turbo · Google Sheets  

## What it does

Automated student support assistant for the ECAM EPMI engineering school —
detects user language, answers questions strictly using verified school data,
and captures unresolved inquiries into a Google Sheet for the admissions team.

## How it works

1. Analyzes the user's initial message using a GPT-3.5-turbo language classifier
   to determine their preferred language (e.g., French, English, Spanish)
2. Searches the official ECAM EPMI knowledge base based on the user's intent
   (e.g., admissions, programs, campus life)
3. Routes into two branches based on the knowledge base results:

**Branch 1 — Answer found in Knowledge Base**
- Synthesizes a short, structured answer using GPT-4o based purely on the retrieved data
- Automatically appends a clickable markdown URL pointing to the exact source page
- Asks exactly one follow-up question to keep the conversation flowing naturally

**Branch 2 — Missing info or human contact requested**
- Triggers a lead capture flow using a GPT-4o-mini confirmation agent
- Asks for the user's full name, email, and a summary of their question
- Validates the email format and confirms details with the user
- Writes the captured lead to a Google Sheet via integration:
  name · email · query

## Why it matters

Fully automates tier-1 student support across multiple languages —
providing instant, accurate answers while ensuring that complex cases
and prospect data are cleanly captured and handed off to human teams.

## Key technical details

- Multi-LLM setup assigns specific models to specialized tasks (GPT-4o, GPT-4o-mini, GPT-3.5-turbo)
- Strict anti-hallucination prompting prevents inventing URLs or quoting outside content
- Custom URL correction logic replaces truncated or general links with verified section roots
- Custom confirmation agent ensures required lead variables are fully collected and validated
- Direct Google Sheets integration pushes rows without needing external automation platforms
