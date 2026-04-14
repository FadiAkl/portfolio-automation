# Apify LinkedIn Outreach System

**Stack** : Make.com · Google Sheets · Apify · OpenAI GPT-4o · Instantly

## What it does

Fully automated cold outreach pipeline that pulls leads from Google Sheets,
scrapes their LinkedIn profiles via Apify, generates a personalized icebreaker
using AI, and pushes the enriched lead into Instantly — ready to send.

## How it works

1. Pulls leads from a Google Sheets spreadsheet
2. Sets multiple variables for each lead:
   - Full name
   - LinkedIn profile URL
   - Company name
   - Role / job title
3. Sends the LinkedIn URL to Apify's LinkedIn Mass Scraper via API module
4. Waits 15 seconds to allow Apify time to complete the scrape
5. Retrieves the dataset output from Apify
6. Extracts the About section from the scraped LinkedIn profile
7. Sends the About section to GPT to generate a personalized icebreaker
8. Pushes the full enriched lead into Instantly via HTTP request:
   - Full name
   - Company name
   - Role
   - LinkedIn URL
   - AI-generated icebreaker

## Why it matters

Eliminates hours of manual research per lead — every contact gets a unique,
profile-based icebreaker automatically, at scale, without touching the data manually.

## Key technical details

- Google Sheets used as the lead source for easy non-technical input
- Apify LinkedIn Mass Scraper handles profile data extraction at scale
- 15s sleep module ensures dataset is ready before retrieval
- GPT processes only the About section to keep icebreakers focused and relevant
- Instantly receives all enriched data via HTTP module for immediate campaign use
