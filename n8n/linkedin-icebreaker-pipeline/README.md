# LinkedIn Icebreaker Pipeline

**Stack** : n8n · Google Sheets · OpenAI · Instantly  

## What it does
1. Pulls leads from a Google Sheets spreadsheet
2. Validates that each lead has a valid email before processing
3. Sends the LinkedIn profile URL to GPT to scrape and extract key information
4. Generates a personalized icebreaker based on the scraped profile data
5. Pushes the enriched lead (email + icebreaker) into Instantly via HTTP request

## Why it matters
Eliminates manual research and copy-paste work for cold outreach —
every lead gets a unique, researched icebreaker automatically.
