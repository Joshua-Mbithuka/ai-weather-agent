# 🌤️ AI Weather Agent

An autonomous AI agent built with **n8n** that fetches real-time weather data and delivers a personalized, AI-written morning briefing to your inbox every day.

---

## 🧠 How It Works

Instead of using a fixed template, this agent uses **Claude (Anthropic)** to read raw weather data and write a natural, conversational briefing — complete with practical tips tailored to the day's conditions.

```
Schedule Trigger (7AM daily)
        ↓
   AI Agent (Claude)
        ↓
  get_weather Tool ←→ OpenWeatherMap API
        ↓
 Gmail (sends email)
```

The key difference from a basic automation: the **AI Agent decides when and how to call the weather tool**, interprets the data, and crafts a unique briefing every morning.

---

## ✨ Sample Output

> Good morning! ☀️ It's a warm start to the day in Nairobi at 22°C, though it feels closer to 24°C with the humidity. Expect moderate rain later in the afternoon, so today's a layering kind of day...

---

## 🛠️ Built With

| Tool | Role |
|------|------|
| [n8n](https://n8n.io) | Workflow automation engine |
| [Claude (Anthropic)](https://anthropic.com) | AI briefing generation |
| [OpenWeatherMap](https://openweathermap.org) | Real-time weather data |
| [Gmail](https://gmail.com) | Email delivery |
| [Railway](https://railway.app) | Cloud hosting (24/7) |

---

## ⚙️ Setup & Installation

### Prerequisites
- n8n instance (local or hosted on Railway)
- Anthropic API key
- OpenWeatherMap API key (free tier)
- Gmail account with OAuth configured

### Steps

**1. Clone this repo**
```bash
git clone https://github.com/YOUR_USERNAME/ai-weather-agent.git
```

**2. Import the workflow into n8n**
- Open your n8n instance
- Click **"New Workflow"** → **"..."** → **"Import from file"**
- Upload `weather-agent.json`

**3. Add your credentials**
- **Anthropic** — Add your API key in the Anthropic Chat Model node
- **OpenWeatherMap** — Replace `Your_WeatherApp_Api_Key` in the `get_weather` tool URL with your key
- **Gmail** — Connect via OAuth in the Gmail node

**4. Configure your city & email**
- In the `get_weather` tool URL, replace `Your_City` with your city name
- In the Gmail node, update the **"To"** field with your email address

**5. Activate the workflow**
- Toggle **Activate** in the top right corner
- The agent will now run every morning automatically ✅

---

## 🏗️ Architecture Details

### Why an AI Agent instead of a template?

A standard automation would fill a fixed message template with weather values. This workflow uses an **agentic pattern** where:

- The AI Agent is given a goal, not a script
- It **calls the weather tool autonomously** when it needs data
- It **interprets and contextualizes** the raw JSON into human-friendly advice
- The output is different every day based on actual conditions

### Nodes breakdown

| Node | Type | Purpose |
|------|------|---------|
| Schedule Trigger | Trigger | Fires workflow at 7AM daily |
| AI Agent | LangChain Agent | Orchestrates tool use and generates briefing |
| Anthropic Chat Model | Language Model | Powers the AI Agent (Claude Haiku 3) |
| get_weather | HTTP Tool | Fetches weather data from OpenWeatherMap |
| Send a message | Gmail | Delivers the briefing via email |

---

## ☁️ Hosting on Railway

This workflow runs 24/7 on [Railway](https://railway.app) using the official n8n + Postgres template.

To deploy your own:
1. Go to [railway.app](https://railway.app) → **New Project** → **Deploy from Template**
2. Search **"n8n"** and deploy
3. Add environment variables for basic auth
4. Import this workflow and add your credentials

---

## 🔐 Security Notes

- API keys and OAuth credentials are **not stored** in the workflow JSON (n8n strips them on export)
- Never commit real API keys to this repo — use placeholders as shown in `weather-agent.json`
- Keep your Railway instance protected with basic auth

---

## 📄 License

JoshuaMbithuka — feel free to fork, modify, and build on this!
