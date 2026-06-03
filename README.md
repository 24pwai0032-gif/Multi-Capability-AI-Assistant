# Multi-Capability AI Assistant

A Python-based AI assistant powered by the Groq API (free tier) that combines three
distinct capabilities and four tools in a single program. Requests are automatically
routed to the right capability based on the input.

---

## What It Does

The assistant handles three types of requests out of the box:

**Enhanced Email Writer** — Describe the email you need and the assistant drafts a
complete, properly structured email with subject line and body. Supports three tones
and can search for market data before writing.

**Smart Summarizer** — Paste any block of text and get a concise summary in your
chosen length. The output includes analytics showing word count, character count,
and how much shorter the summary is compared to the original.

**Chat Assistant** — A general-purpose conversational AI with persistent memory.
It remembers everything said earlier in the session and can answer follow-up questions
naturally. It also has access to all four tools during chat.

---

## Capabilities

| # | Capability | What It Does |
|---|-----------|--------------|
| 1 | Enhanced Email Writer | Drafts emails in formal, friendly, or casual tone. Optionally researches a topic via web search before writing. |
| 2 | Smart Summarizer | Summarizes text in short (1 sentence), medium (2-3 sentences), or long (4-5 sentences) format. Shows word count reduction stats. |
| 3 | Chat Assistant | Conversational chat with full memory of the session. Uses tools automatically when needed. |

---

## Tools

| # | Tool | Description |
|---|------|-------------|
| 1 | Calculator | Evaluates math expressions safely. Supports +, -, *, /, **, sqrt, log, trig, pi, e. |
| 2 | Web Search | Mock web search returning realistic results for business, AI, tech, climate, and general topics. |
| 3 | Data Analyzer | Computes sum, average, max, min, median, and standard deviation for any list of numbers. |
| 4 | Weather | Returns current weather for Pakistani cities (Karachi, Lahore, Islamabad, Multan, Peshawar, Quetta) and major global cities. |

---

## Requirements

- Python 3.9 or higher
- A free Groq API key — get one at https://console.groq.com

---

## Installation

```bash
# 1. Clone the repository
git clone https://github.com/your-username/my-ai-assistant.git
cd my-ai-assistant

# 2. Install dependencies
pip install -r requirements.txt

# 3. Set up your API key
cp .env.example .env
# Open .env and replace the placeholder with your real Groq API key
```

---

## Running the Assistant

```bash
python assistant.py
```

This starts the interactive chat loop. Type your request and press Enter.

**Special commands inside the chat:**

| Command | What It Does |
|---------|--------------|
| `exit` or `quit` | Stop the session |
| `history` | Show the full conversation so far |
| `clear` | Wipe conversation memory and start fresh |
| `help` | Show usage examples for all features |

---

## Usage Examples

### Email Writer

Type anything that includes "write email", "draft email", or "compose email":

```
Write a formal email to stakeholders announcing our Q2 sales results
Draft a friendly email to the team about the upcoming office party
Compose a casual email asking for a deadline extension
```

The assistant detects the tone (formal / friendly / casual) and recipient type
(client / team / stakeholder / supplier) from your message automatically.

To include web research before writing, add "research" to your message:
```
Write a friendly email to clients introducing our AI product with research
```

### Summarizer

Type "summarize:" followed by your text:

```
Summarize: [paste your paragraph or article here]
Short summarize: [text]       -- produces a single sentence
Long summarize: [text]        -- produces 4-5 sentences
```

### Chat with Tools

Ask anything conversationally. The assistant uses tools automatically:

```
What is 15% of 8500?
Analyze these monthly sales figures: 45000, 52000, 61000, 70000, 80000
What is the weather in Islamabad today?
Search for the latest AI trends
What is the capital of Pakistan?
```

The assistant remembers earlier messages, so follow-up questions work:

```
You:        My name is Ahmed and I work in sales.
Assistant:  Nice to meet you, Ahmed! ...
You:        What is my job?
Assistant:  You work in sales, Ahmed.
```

### Auto-Router

The `process()` method automatically routes any input to the right capability.
You can call it directly in code:

```python
from assistant import MultiCapabilityAssistant
import os

assistant = MultiCapabilityAssistant(api_key=os.environ["GROQ_API_KEY"])

# Routes to Email Writer
print(assistant.process("Write a formal email to thank a supplier"))

# Routes to Summarizer
print(assistant.process("Summarize: [your text here]"))

# Routes to Chat (fallback)
print(assistant.process("Explain what machine learning is"))
```

---

## File Structure

```
my-ai-assistant/
├── assistant.py        Main program
├── requirements.txt    Python dependencies
├── .env.example        API key template
├── examples.txt        Sample inputs and expected outputs
└── README.md           This file
```

---

## Getting a Free Groq API Key

1. Go to https://console.groq.com
2. Sign up for a free account
3. Navigate to **API Keys** and create a new key
4. In Google Colab: click the lock icon (Secrets panel) and add a secret named `groq`
5. In a local project: paste the key into your `.env` file

---

## Model

This assistant uses `llama-3.3-70b-versatile` via the Groq API. It is available
on the free tier with generous rate limits, making it suitable for development
and coursework.

---

*Built for atomcamp Agentic AI Bootcamp — Session 2 Assignment*
