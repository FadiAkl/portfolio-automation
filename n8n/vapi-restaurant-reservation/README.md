# Vapi Restaurant Reservation System

> 🚧 Work in progress — Cancel branch and unavailable slot handling are still being built.

**Stack** : n8n · Vapi · Google Calendar · JavaScript

## What it does

An n8n backend that powers a Vapi voice AI assistant for a restaurant called
"Luxury Estate". The voice assistant handles the full conversation with the
customer, then fires tool calls to this n8n webhook to manage reservations
directly on Google Calendar in real time.

## How it works

The workflow is triggered by a webhook receiving tool call requests from Vapi,
then routes them into three branches based on the action requested:

**Schedule (booking a new reservation)**
1. Receives the booking time and customer name from the Vapi voice call
2. Checks Google Calendar for busy slots in the requested 1-hour window
3. Runs a JavaScript conflict check against the busy list
4. If available → creates the event on Google Calendar
5. Sends a confirmation response back to Vapi with the booking details

**Reschedule (modifying an existing reservation)**
1. Fetches existing events between the current and new appointment times
2. Filters to find the relevant event
3. Runs a JavaScript availability check for the new requested time
4. If available → creates the updated event on Google Calendar
5. *(Unavailable path — in progress)*

**Cancel**
1. *(In progress)*

## Vapi assistant details

- Model: GPT-4o-mini
- Voice: ElevenLabs (eleven_multilingual_v2)
- Transcription: Deepgram Nova-3
- The assistant collects name, date/time, party size, and phone number
  before triggering any tool call
- All three actions (Schedule, Reschedule, Cancel) route to the same
  n8n webhook and are separated by a Switch node

## Key technical details

- Webhook-triggered instantly via Vapi tool calls
- Custom JavaScript used for conflict detection and time zone handling (Europe/Paris)
- Google Calendar used as the live source of truth for availability
- Vapi receives structured JSON responses back from n8n after each action
