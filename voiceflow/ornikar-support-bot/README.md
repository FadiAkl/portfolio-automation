# Ornikar Customer Support Chatbot (Ornibot)

**Stack** : Voiceflow · Claude (Sonnet 4 + Haiku 3.5) · Elevenlabs TTS · Calendly · Airtable · RAG Intent Classification

## What it does

An AI-powered customer support chatbot that handles full appointment management for a French driving school —
booking lessons, answering pricing questions, providing exam information, and escalating to human agents —
all connected to Calendly and Airtable in real time.

## How it works

The chatbot listens for user intents via natural language understanding and routes them into five primary branches:

**Branch 1 — Provide Information**
- Receives customer questions about driving school services
- Uses Claude with RAG (Retrieval-Augmented Generation) to search the knowledge base
- Routes queries to specialized prompt chains: pricing, code training, driving lessons, or general info
- Maintains a conversational French tone with a maximum 2-sentence response limit
- Suggests sign-up links only when contextually relevant

**Branch 2 — Book Appointment**
- Triggered when the user expresses intent to schedule a lesson or consultation
- Collects customer name and email via form capture
- Generates a Calendly link with name/email pre-populated as URL parameters
- Displays an interactive calendar directly within the chatbot
- Stores the booking request in Airtable for CRM tracking

**Branch 3 — Schedule Lesson/Exam Info**
- Provides real-time information about exam dates, requirements, and availability
- Explains minimum hours required (20 for manual, 13 for automatic)
- Details cancellation policies (48 hours notice required)
- Offers next available exam slot suggestions

**Branch 4 — Transfer to Human Agent**
- Triggered on "Parler à un humain" (speak to human) intent
- Collects customer information (name, email)
- Escalates to a live agent via contact form
- Stores interaction history in Airtable to provide the agent with full context
- Provides confirmation that a representative will contact them within the SLA

**Branch 5 — Handle Follow-ups**
- After each response, prompts the user: "Avez-vous d'autres questions ?" (Any other questions?)
- Routes to loop back to information provision or exit the conversation
- Tracks multi-turn conversations in memory (25-turn limit)

## Why it matters

Fully automates tier-1 support and bookings for a busy driving school —
delivering instant answers, generating pipeline through embedded scheduling,
and ensuring human agents only handle complex escalations with full context already collected.

## Key technical details

- Webhook-triggered via Voiceflow intent recognition using Claude 3.5-Haiku classification engine
- Claude 4 Sonnet used for complex reasoning, knowledge retrieval, and conversational generation
- RAG integration with a knowledge base containing 100+ pricing tiers, policy details, and FAQ answers
- Real-time Calendly embedding via iframe injection into the chatbot response
- Airtable API integration (POST requests) for persistent CRM data storage (Fields: Name, Email, Status, Problem Description)
- Elevenlabs TTS (eleven_turbo_v2_5 model) for voice-enabled interactions
- Variable system captures: Name, Email, last_utterance, vf_memory (10-turn conversation history), intent_confidence score
- Handles edge cases: No match on intents, form validation errors, Airtable sync failures with fallback paths
- Multi-language support for French/English with locale-aware responses
- Shareable link with password protection for demo access (password: 1234)
