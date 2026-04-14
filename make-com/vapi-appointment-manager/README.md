# Vapi AI Voice Appointment Manager

**Stack** : Make.com · Vapi · OpenAI GPT-4o · Google Calendar  

## What it does

An AI voice assistant powered by Vapi that handles full appointment management
over the phone — booking, rescheduling, and cancellation — all connected to
Google Calendar in real time.

## How it works

The workflow listens for incoming tool calls from the Vapi voice assistant
and routes them into three branches:

**Schedule**
1. Receives the requested booking time and customer name from the voice call
2. Uses GPT-4o to generate a 72-hour availability window around the requested date
3. Checks Google Calendar for busy slots within that window
4. If available → creates the event directly on Google Calendar
5. If unavailable → finds the next open slot and suggests it back to the caller

**Reschedule**
1. Searches Google Calendar for the existing appointment
2. Checks if the new requested time is available
3. If available → updates the event
4. If unavailable → suggests the next open slot

**Cancel**
1. Searches Google Calendar for the appointment at the specified time
2. If found → deletes the event and confirms cancellation
3. If not found → informs the caller that no appointment exists

## Key technical details

- Webhook-triggered (instant) via Vapi tool calls
- GPT-4o used for date parsing, availability checking, and conflict resolution
- All responses sent back to Vapi in real time via webhook response
- Handles edge cases: slot conflicts, appointment not found, wrong time provided
