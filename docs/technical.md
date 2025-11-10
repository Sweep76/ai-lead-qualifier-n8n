# 🧠 User Documentation (Technical Users)

## Overview
This documentation is intended for developers, engineers, and technical users who wish to deploy, extend, or maintain the **AI-Powered Lead Qualification and Response Workflow**.  
The system is built using **n8n**, **OpenAI**, **Google APIs**, and **Discord Webhooks**.

The workflow automates:

1. Lead retrieval from **Google Sheets**
2. Lead analysis and email drafting via **OpenAI**
3. Reply sending through **Gmail**
4. Internal notifications via **Discord Webhook**



## ⚙️ Technical Prerequisites

### Environment
- **n8n** (Local, Self-hosted, or Cloud)
- **Node.js 18+** (for local setup)
- **Google Cloud Project** with:
  - Google Sheets API  
  - Google Drive API  
  - Gmail API  
- **Active OpenAI API key**
- **Discord Webhook URL**

---

### Credential Setup

| Service | Auth Type | Notes |
|----------|------------|-------|
| Google Sheets | OAuth2 | Redirect URI: `http://localhost:5678/rest/oauth2-credential/callback` |
| Gmail | OAuth2 | Same redirect URI, scope: `https://www.googleapis.com/auth/gmail.send` |
| OpenAI | API Key | Get it from [https://platform.openai.com/api-keys](https://platform.openai.com/api-keys) |
| Discord | Webhook | Create from *Server Settings → Integrations → Webhooks* |

---

## 🧩 Node-by-Node Workflow Description

| Node | Type | Purpose |
|------|------|----------|
| **Google Sheets – Get Lead** | Google Sheets | Retrieves rows with columns: `timestamp`, `name`, `email`, `company`, `budget`, `use_case`, `message`. |
| **OpenAI – Analyze Lead** | OpenAI Chat Model | Processes each row and returns JSON with `priority`, `summary`, and `personalized_email`. |
| **Function – Parse Output** | Function Node | Parses JSON from OpenAI (`output[0].content[0].text`) and normalizes data. |
| **Gmail – Send Reply** | Gmail | Sends `personalized_email` to the corresponding `email` address. |
| **Discord – Notify Lead** | HTTP Request | Sends formatted message to a Discord channel using the Webhook URL. |

---

## 🧠 Key Expressions

### Gmail Node
**To:**
```text
{{$node["Google Sheets - Get Lead"].json["email"]}}
{{$json["personalized_email"]}}
```

Discord WebHook Message
```
🧠 New {{$json["priority"]}} priority lead  
👤 {{$node["Google Sheets - Get Lead"].json["name"]}} ({{$node["Google Sheets - Get Lead"].json["email"]}})  
🏢 {{$node["Google Sheets - Get Lead"].json["company"]}}  
📝 {{$json["summary"]}}
```

## Project Structure
```
ai-lead-qualifier-n8n/
├─ workflow/
│  └─ ai-lead-qualifier-n8n.json
├─ docs/
│  ├─ technical.md
│  ├─ nontechnical.md
└─ README.md
```
## 🚀 Setup Steps

### 1. Import Workflow
In **n8n**, go to **Workflows → Import from File** → select `ai-lead-qualifier-n8n.json`.

### 2. Connect Credentials
Link your credentials for:
- **Google Sheets**
- **Gmail**
- **OpenAI**
- **Discord Webhook**

### 3. Update Sheet Reference
Point the **Google Sheets** node to your active sheet containing the lead data.

### 4. Run Workflow
Execute the workflow manually once to verify the end-to-end automation flow.

### 5. Optional Automation
Add a **Cron** or **Google Sheets Trigger** node to automatically execute the workflow when new rows are added.

---

## ⚡ Scalability Ideas

- 🔁 Replace manual **Get Rows** with a **Trigger Node** for real-time automation.  
- 🚨 Add **IF nodes** for `priority === "High"` to alert the sales team.  
- 🗃️ Store results in a **database** for long-term analytics and reporting.  
- 🤝 Integrate with **CRM tools** such as HubSpot or Notion for deeper workflow automation.

---

**Workflow Version:** v1.0 – *AI Lead Qualifier (n8n)*  
**Maintainer:** Joshua Patrick G. Chiu  
**Email:** joshuapatrickchiu76@gmail.com


