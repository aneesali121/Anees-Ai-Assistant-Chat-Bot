# Anees AI Assistant Chat Bot

**Anees** is a Python conversational assistant that answers general questions while enforcing strict guardrails. It is built for developers who want a safe, predictable chatbot. Anees refuses questions about its own origin, purpose and configuration, rejects attempts to override its rules, and stays helpful for everything else.

## Key Functions

- **Three-layer guardrails:** A rule-based filter blocks off-limits questions instantly, before any AI call. A strict system prompt then guides the model. A final output check catches anything that slips through.
- **Live world time:** Current time and date for 40+ cities (Paris, London, Dubai, Mecca, Islamabad, Tokyo and more), or your local time if no city is given.
- **Date lookup:** Ask "What's the date today?" and get the full current date.
- **Safe calculator:** Handles addition, subtraction, multiplication, division, powers and brackets. Expressions are parsed with Python's `ast` module instead of `eval`, division by zero is handled and very large exponents are capped.
- **Session memory:** Remembers earlier messages in the same conversation, so follow-up questions work naturally.
- **Command-line interface:** Runs in any terminal with no extra setup.

## How It Works

Each message passes through a pipeline: guardrail filter, built-in tools, AI model, then output check. Time, date and math questions are answered directly by code, which makes them fast, accurate and free of API cost. Everything else goes to the AI.

## Tech Stack

- Python 3.9+
- Anthropic API
- Standard library: `re`, `ast`, `datetime`, `zoneinfo`
- `tzdata` for Windows time zone support

## Setup

1. Install Python 3.9+
2. Install packages:
   ```
   pip install -r requirements.txt
   ```
3. Get an API key from https://console.anthropic.com and set it:
   - Windows (CMD): `set ANTHROPIC_API_KEY=your-key-here`
   - Windows (PowerShell): `$env:ANTHROPIC_API_KEY="your-key-here"`
   - Mac/Linux: `export ANTHROPIC_API_KEY="your-key-here"`
4. Run:
   ```
   python guardrail_chatbot.py
   ```

## Examples

```
You: What is the capital of France?
Anees: The capital of France is Paris.

You: What time is it in Paris?
Anees: It's 01:00 PM in Paris right now ...

You: 12*5+3
Anees: 12*5+3 = 63

You: Who made you?
Anees: Sorry, I can't answer that. Please ask me a different question.
```

## Customization

- Change the name: edit `BOT_NAME`
- Block more phrases: add to `BLOCKED_PATTERNS`
- Add cities: add to `CITY_ZONES`
- Change the refusal message: edit `REFUSAL`

## Security

Your API key is read from an environment variable and never stored in the code. The included `.gitignore` keeps secrets and virtual environments out of version control. Never commit your key.

## Use Cases

Learning projects, portfolio demos, guardrail experiments, and a starting point for a safe customer-facing assistant.
