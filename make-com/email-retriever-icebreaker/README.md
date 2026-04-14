# Email Retriever & Icebreaker Generator

**Stack** : Make.com · Google Sheets · AnyMailFinder · OpenAI GPT-3.5 · Google Sheets  

## What it does

Automated cold outreach pipeline targeting French driving school owners —
filters leads, finds their professional email, generates a personalized
French icebreaker, and sorts results into two separate output sheets.

## How it works

1. Pulls leads from a Google Sheets spreadsheet ("Auto Ecole Info")
2. Filters only driving school leads — only processes rows where the
   company name contains keywords like "auto", "conduite", "automobile", or "permis"
3. Sends the lead's full name to GPT to clean and format it
   (removes emojis, fixes capitalization)
4. Stores key variables for the lead:
   - Full name
   - Company name
   - Job title
   - LinkedIn summary
   - Title description
   - Company location
5. Routes into two branches based on email lookup result:

**Branch 1 — Email found**
- Calls AnyMailFinder API with the lead's name + company to find their professional email
- If email is found (status 200) → sends profile data to GPT to generate
  a personalized French icebreaker based on the LinkedIn summary
- Writes the enriched lead to a "Leads email" Google Sheet:
  name · company · title · icebreaker · email

**Branch 2 — No email found**
- Writes basic lead info to a separate "basicinfo" Google Sheet:
  name · company · title · location
- Keeps unresolved leads organized for manual follow-up

## Why it matters

Fully automates the most time-consuming part of cold outreach —
finding verified emails and writing personalized openers —
while keeping clean records of both successful and unresolved leads.

## Key technical details

- Keyword filter ensures only relevant driving school leads are processed
- GPT name formatting handles messy LinkedIn exports (emojis, bad capitalization)
- AnyMailFinder used for professional email discovery via API
- Router logic separates enriched leads from dead ends automatically
- All icebreakers written in French, casual and personalized to each profile
