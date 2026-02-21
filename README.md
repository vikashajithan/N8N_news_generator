# 📰 AI Newsletter Bot (n8n + Slack + OpenAI)

An automated AI-powered newsletter generator built using **n8n Cloud**, **Slack**, **OpenAI**, and a News Search API (Serper / NewsAPI).

This workflow listens to Slack messages, detects news-related requests, fetches real-time news, generates a structured newsletter using AI, and delivers it via Slack and Gmail.

---

## 🚀 Features

- ✅ Slack-triggered automation  
- ✅ Strict news-only detection (not a chatbot)  
- ✅ AI topic extraction  
- ✅ Real-time news fetching  
- ✅ AI-generated formatted newsletter  
- ✅ Slack message delivery  
- ✅ Gmail email delivery  
- 🔄 Extendable with memory & personalization  

---

## 🏗 Workflow Architecture

Slack Trigger  
→ Basic LLM Chain (Intent & Topic Detection)  
→ IF (is_news === true)  
→ HTTP Request (News Search API)  
→ Basic LLM Chain (Newsletter Generation)  
→ Slack Send Message  
→ Gmail Send Message  

---

## 🧠 How It Works

### 1️⃣ Slack Trigger
- Listens to messages in a selected Slack channel.
- Workflow must be **activated** (production mode).

Example user messages:
```
AI news
US tariff news
Crypto updates
```

---

### 2️⃣ Intent Classification (OpenAI)

The first LLM node:
- Detects if the message is about news
- Extracts the topic

Example output:
```json
{
  "is_news": true,
  "topic": "US tariff"
}
```

If `is_news` is false → workflow stops.

---

### 3️⃣ Conditional Routing

IF node:
- TRUE → Continue
- FALSE → Stop

Ensures the bot only handles newsletters.

---

### 4️⃣ News Fetching

Uses HTTP Request node with dynamic query:

```
q = extracted topic
```

Supports:
- NewsAPI
- Serper (Google News API)
- Any external news API

---

### 5️⃣ Newsletter Generation

Second LLM node:
- Converts raw news articles into:
  - Title
  - Introduction
  - 5 summarized bullet headlines
  - Closing message

Clean, professional formatting.

---

### 6️⃣ Delivery

The newsletter is sent via:

- Slack (channel message)
- Gmail (email send)

---

## ⚙️ Required Credentials

### Slack
- Bot Token
- Signing Secret
- Event Subscriptions enabled
- Bot invited to channel

### OpenAI
- API Key
- Recommended model: `gpt-4o-mini`

### News API / Serper
- API key (if using external provider)

### Gmail (optional)
- OAuth2 credentials

---

## 🔧 Setup Instructions

1. Import workflow into n8n
2. Configure credentials
3. Activate workflow
4. Invite Slack bot to channel
5. Send test message in Slack

---

## 📌 Example Output

User sends:
```
AI news
```

Bot replies:

```
📰 AI Weekly Update

This week in artificial intelligence...

• OpenAI releases new model...
• Google expands AI research...
• Startup funding increases...
• AI regulation discussions grow...
• Enterprise AI adoption rises...

Stay tuned for more updates!
```

---

## 🔒 Strict Mode Behavior

This workflow is NOT a chatbot.

It only:
- Detects news-related requests
- Generates newsletters
- Ignores general questions

---

## 🛠 Future Improvements

- Add Data Store memory
- Add vector-based personalization
- Prevent duplicate same-day newsletters
- Track user interests
- Add scheduled daily digests
- Format using Slack Block Kit
- Add analytics tracking

---

## 🧩 Tech Stack

- n8n Cloud
- Slack API
- OpenAI Chat Models
- News Search API (Serper / NewsAPI)
- Gmail API

---

## 📄 License

Internal automation project.  
Modify and extend as needed.
