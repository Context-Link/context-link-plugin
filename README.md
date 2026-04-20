# Context Link Plugin

Connect Claude to your [Context Link](https://context-link.ai) knowledge base and retrieve just the right context from your connected sources: Notion, Google Drive and any websites. Context Link also has a memory layer where you can save conversation insights, documents and anything else you want to persist directly from an AI interaction.

## What it does

- **Get Context** — Pull relevant knowledge from your Context Link when you reference internal topics
- **Ask Question** — Get a concise, cited answer grounded in your Context Link (Pro plan)
- **Save Memory** — Save conversation content to Context Link for later retrieval
- **Update Memory** — Retrieve existing saved content, merge in new information, and save it back

## Components

### Skills (auto-triggered)

| Skill | Triggers when you... |
|-------|---------------------|
| `get-context` | Semantic search which returns the most relevant content for any topic, no exact matches required. Just ask for 'context' on whatever you need. |
| `ask-question` | Say "ask my context", "ask Context Link what…", or ask a direct question to be answered from your knowledge base with citations (Pro plan) |
| `save-memory` | Say "save to Context Link under /topic_123", "save this chat to Context Link", or ask to store information |
| `update-memory` | Say "update this memory in Context Link under /topic_456" |

### Commands (manual)

| Command | Usage |
|---------|-------|
| `/get-context [topic]` | Retrieve knowledge about a specific topic |
| `/ask-question [question]` | Get a short, cited answer grounded in your Context Link (Pro plan) |
| `/save-memory [slug]` | Save something under a specific name, or a summary of the chat to an auto generated name (chat-session-{YYYY-MM-DD-HHMM}) |
| `/update-memory [slug]` | Update existing saved content with new info |

## Setup

After installing the plugin, you'll need to customize it with your personal Context Link URL:

1. Sign in at [context-link.ai](https://context-link.ai)
2. Your URL is shown at the top of every screen — it looks like `https://yourname.context-link.ai/TOPIC_HERE?p=xyz`
3. Copy and paste it exactly as shown — no editing needed
4. The plugin customizer will ask you to replace `~~context link url~~` with your URL

## How it works

Context Link is a knowledge base that indexes your content (websites, Google Drive, Notion) into searchable embeddings. This plugin lets Claude query that knowledge and save new content back, using Context Link's REST API.

- **GET** `{your-url}/{topic}` — retrieves content matching the topic
- **GET** `{your-url}/q/{question}` — returns a grounded, cited answer to the question
- **POST** `{your-url}/{slug}` — saves markdown content under a named slug
