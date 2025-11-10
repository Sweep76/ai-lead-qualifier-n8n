# 💼 User Documentation (Non-Technical Users)

# Overview
This automation helps your team respond faster and more consistently to client inquiries.  
It reads new entries from a shared Google Sheet, uses AI to understand each message, and automatically:

1. Sends a personalized email reply to the customer.  
2. Notifies your internal team in Discord with a short summary.

You don’t need any technical setup once it’s configured.

---

## How It Works

| Step | What Happens | Example |
|------|-------------|---------|
| 1️⃣ | Customer submits a form. | “Hi, can you help automate our sales report generation?” |
| 2️⃣ | Response is saved to Google Sheets. | A new row appears with name, email, company, and message. |
| 3️⃣ | n8n detects the new entry. | The workflow fetches the latest row. |
| 4️⃣ | AI analyzes the details. | Assigns **High priority** and writes a personalized reply. |
| 5️⃣ | Gmail sends the message automatically. | The customer receives a tailored email reply. |
| 6️⃣ | Discord posts a summary. | The team sees a quick notification in `#ai-leads`. |

---

## Benefits

- ⚡ **Faster Replies:** Customers get an immediate, relevant response.  
- 🧠 **AI Quality:** Replies are professional and consistent.  
- 🔔 **Team Alerts:** Everyone is notified instantly on Discord.  
- 🕒 **Time Savings:** Reduces manual review hours.  
- 💬 **No Missed Leads:** Every submission gets a response.

---

## How To Use It

1. Continue using your existing Google Form (linked to the Sheet).  
2. Check your Gmail **Sent** folder for automatic replies.  
3. Monitor the Discord channel for new lead summaries.  
4. For important leads, follow up manually as needed.

---

## Troubleshooting

If you stop seeing emails or Discord messages:

| Issue | What to Check |
|-------|----------------|
| No emails sent | Gmail credential expired — reconnect it in n8n. |
| AI not responding | Verify your OpenAI API key is still active. |
| No Discord updates | Check if your Webhook URL changed. |
| Sheet changed | Ensure the column names remain the same. |

---

## Contact

**Workflow Owner:** Joshua Patrick G. Chiu  
**Email:** joshuapatrickchiu76@gmail.com  
**Workflow Version:** v1.0 – *AI Lead Qualifier (n8n)*
