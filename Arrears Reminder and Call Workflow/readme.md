# Arrears Reminder and Call Workflow

This n8n workflow automates payment reminders and voice AI calls for overdue customers. It integrates multiple services to provide intelligent payment collection automation with AI-driven analysis and follow-up actions.

---

## 🔧 Prerequisites

To set up the system, you need:

- **n8n account** – Cloud or self-hosted instance for workflow automation
- **OpenAI API key** – For AI-driven analysis and responses
- **VAPI account** – For voice AI calls with webhook integration
- **Email service** – Gmail, SendGrid, or similar SMTP-enabled platform
- **Google Sheets API** – For data tracking and reporting

---

## 🚀 Installing n8n

You can install and run n8n either using **npx** or **Docker**.

### Option 1: Install via NPX (local machine)

```bash
npx n8n
```

> This starts n8n locally on [http://localhost:5678](http://localhost:5678)

### Option 2: Run with Docker

Create a simple `docker-compose.yml`:

```yaml
version: '3.1'

services:
  n8n:
    image: n8nio/n8n
    restart: always
    ports:
      - 5678:5678
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=<your_user>
      - N8N_BASIC_AUTH_PASSWORD=<your_password>
    volumes:
      - ./n8n:/home/node/.n8n
```

Start with:

```bash
docker-compose up -d
```

Then access it via [http://localhost:5678](http://localhost:5678)

---

## 🔑 Credential Setup

### 1. OpenAI API

Create an OpenAI credential in n8n using your API key:

👉 [OpenAI Credential Setup](https://docs.n8n.io/integrations/builtin/credentials/openai/)

Ensure you've selected the correct model (e.g., `gpt-4`, `gpt-3.5-turbo`, etc.) in the workflow.

### 2. vAPI Account

Set up your vAPI credentials for voice AI calls:

1. Create a vAPI account at [vapi.ai](https://vapi.ai)
2. Generate API key from your dashboard
3. Configure webhook endpoints for call completion callbacks
4. Add vAPI credentials to n8n as HTTP Header Auth

### 3. Email Service Setup

#### Gmail OAuth

Follow the official guide to set up Gmail credentials:

👉 [Gmail OAuth Setup Guide](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)

 
### 4. Google Sheets API

Configure Google Sheets for data tracking:

👉 [Google Sheets API Setup](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)

Required GOOGLE API SERVICE:
- `Google Drive API`
- `Google Sheet API`

---

## 🔄 Workflow Overview

### 1. Payment Reminder and Call Trigger

**Webhook Trigger**
- Receives customer payment data from your billing system
- Processes customer information, payment status, and due dates

**Decision Logic**
- Checks due dates and overdue status
- Determines appropriate action based on payment stage

**Email Notifications**
- **Gentle reminder** (2 days before due)
- **Overdue notice** (on due date)
- **Final notice** (after due date)

**Voice AI Call Trigger**
- Activates if emails don't resolve the payment
- Initiates vAPI call with customer context

### 2. Post-Call Analysis and Follow-Up

**vAPI Webhook Processing**
- Receives call completion data from vAPI
- Processes call duration, status, and transcript

**AI Analysis**
- Extracts actionable insights from conversation transcripts
- Identifies customer intent and payment commitments
- Generates recommended follow-up actions

**Automated Actions**
- Send payment links via email/SMS
- Update Google Sheets tracking data
- Schedule additional follow-ups based on AI analysis
- Create calendar reminders for staff

---

## 📥 Importing the Workflow

To import this workflow into n8n:

1. Open [http://localhost:5678](http://localhost:5678) (or your n8n instance)
2. Click on the **menu icon (☰)** in the top right
3. Choose **Import Workflow**
4. Select the `Arrears Reminder and Call Workflow.json` file
5. Click **Import**

Once imported, make sure to:

* Link the proper **credentials** to each service node
* Configure webhook URLs for vAPI integration
* Set up Google Sheets template with required columns
* Test each connection before activating the workflow

---

## ⚙️ Configuration

### Required Google Sheets Columns

Set up your tracking spreadsheet with these columns:

- Customer ID
- Customer Name
- Email
- Phone Number
- Amount Due
- Due Date
- Payment Status
- Last Contact Date
- Call Status
- AI Analysis Summary
- Next Action
- Follow-up Date

 
### Email Templates

Customize email templates in the workflow nodes:

- **Gentle Reminder**: Friendly payment reminder
- **Overdue Notice**: More urgent tone with payment options
- **Final Notice**: Clear consequences and immediate action required

---

## 🔍 Monitoring and Analytics

### Execution Monitoring

- Monitor workflow executions via the **Executions** panel
- Track success/failure rates for email delivery
- Monitor vAPI call completion rates

### Data Analytics

Use the Google Sheets integration to track:

- Payment collection rates
- Email response effectiveness
- Call success rates
- Average time to payment resolution

---

## 🛠️ Troubleshooting

### Common Issues

1. **Webhook not receiving data**
   - Verify webhook URL configuration
   - Check n8n instance accessibility
   - Validate incoming data format

2. **vAPI calls not triggering**
   - Confirm vAPI API key is valid
   - Check webhook configuration
   - Verify phone number format

3. **Email delivery failures**
   - Check email service credentials
   - Verify recipient email addresses
   - Monitor spam/bounce rates

### Testing

Before going live:

1. Test webhook with sample data
2. Send test emails to verify delivery
3. Make test vAPI calls
4. Verify Google Sheets updates
5. Test AI analysis with sample transcripts

---

## ✅ Final Steps

* Activate the workflow using the **"Activate"** toggle in the editor
* Configure your billing system to send webhook data
* Set up monitoring alerts for failed executions
* Train your team on the new automated process

---

## 📎 References

* [n8n Docs](https://docs.n8n.io/)
* [vAPI Documentation](https://docs.vapi.ai/)
* [OpenAI API Documentation](https://platform.openai.com/docs)
* [Google Sheets API](https://developers.google.com/sheets/api)
* [n8n Community Forum](https://community.n8n.io/)

---

## 📞 Support

For workflow-specific questions or customization requests, please refer to your internal documentation or contact your automation team.