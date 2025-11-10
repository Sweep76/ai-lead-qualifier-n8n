# 🤖 AI Lead Qualifier (n8n Workflow)

An **AI-powered automation workflow** built with **n8n**, **OpenAI**, **Google Sheets**, **Gmail**, and **Discord Webhooks** to automatically qualify leads, draft personalized responses, and notify your team — all without manual intervention.

---

## 📘 Overview

The **AI Lead Qualifier** streamlines customer communication by connecting multiple apps and APIs. It automatically reads form submissions from Google Sheets, uses AI to analyze and prioritize leads, sends personalized email replies, and posts summary alerts to a Discord channel.

### ✨ Features
- 📥 **Automated Lead Intake** – Reads new rows from a connected Google Sheet.  
- 🧠 **AI Analysis** – Uses OpenAI to classify lead priority and generate summaries.  
- 📧 **Smart Replies** – Sends context-aware, personalized emails via Gmail.  
- 🔔 **Team Notifications** – Posts summarized lead info in Discord for visibility.  
- ⚙️ **Fully Customizable** – Modify node logic, triggers, or integrations as needed.

---

## 🧩 Workflow Overview

| Node | Type | Description |
|------|------|--------------|
| **Google Sheets – Get Lead** | Google Sheets | Retrieves new leads (name, email, company, budget, use case, message). |
| **OpenAI – Analyze Lead** | OpenAI Chat Model | Analyzes each row to assign a priority and generate email content. |
| **Function – Parse Output** | Function Node | Parses the JSON response from OpenAI (`output[0].content[0].text`). |
| **Gmail – Send Reply** | Gmail | Sends the AI-generated personalized email to the client. |
| **Discord – Notify Lead** | HTTP Request | Posts summary details to a designated Discord channel via Webhook. |

---

## ⚙️ Requirements

### Environment
- [n8n](https://n8n.io) (Cloud, Local, or Self-hosted)  
- Node.js **v18+** (for local setup)  
- A **Google Cloud Project** with the following APIs enabled:
  - Google Sheets API  
  - Google Drive API  
  - Gmail API  
- Active **OpenAI API Key**  
- **Discord Webhook URL**

---

### Credential Setup

| Service | Auth Type | Notes |
|----------|------------|-------|
| Google Sheets | OAuth2 | Redirect URI: `http://localhost:5678/rest/oauth2-credential/callback` |
| Gmail | OAuth2 | Scope: `https://www.googleapis.com/auth/gmail.send` |
| OpenAI | API Key | Get from [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys) |
| Discord | Webhook | Create via *Server Settings → Integrations → Webhooks* |

---

## 🚀 Setup Steps

### 1. Import Workflow  
In **n8n**, go to **Workflows → Import from File** → select `ai-lead-qualifier-n8n.json`.

### 2. Connect Credentials  
Link your **Google Sheets**, **Gmail**, **OpenAI**, and **Discord** credentials.

### 3. Update Sheet Reference  
Point the **Google Sheets** node to your active leads spreadsheet.

### 4. Run Workflow  
Execute manually once to verify the end-to-end flow works correctly.

### 5. Optional Automation  
Add a **Cron Trigger** or **Google Sheets Trigger** to automatically run on new form submissions.

---