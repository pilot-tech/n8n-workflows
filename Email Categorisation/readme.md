# Email Categorisation Workflow

This n8n workflow automatically categorizes incoming Gmail emails using AI analysis and routes them to appropriate channels with intelligent labeling and Slack notifications.

---

## 🚀 How to Use This Workflow in n8n

### Step 1: Install n8n

You can run n8n locally using either method below. [N8N Documentation](https://docs.n8n.io/)

```bash
npx n8n
```

Access at: [http://localhost:5678](http://localhost:5678)

Alternatively, use n8n Cloud for a hosted solution: [n8n.cloud](https://n8n.cloud)

### Step 2: Import the Workflow

1. **Download the Workflow JSON**
   
   (Replace with your hosted .json file link)

2. Open your n8n instance at [http://localhost:5678](http://localhost:5678)

3. Click the **☰ menu** in the top-right

4. Choose **Import Workflow**

5. Select the downloaded `.json` file

6. Click **Import**

### Step 3: Set Up Required Credentials

Each service node in the workflow needs credentials configured in n8n.

#### Gmail OAuth

Use this guide to configure:
👉 [Gmail OAuth Setup](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)

#### OpenAI API Key

Guide:
👉 [OpenAI Setup Guide](https://docs.n8n.io/integrations/builtin/credentials/openai/)

Select the appropriate model: `gpt-4` or `gpt-3.5-turbo`

#### Slack OAuth

Set up via:
👉 [Slack Integration Guide](https://docs.n8n.io/integrations/builtin/credentials/slack/)

Required scopes: `chat:write`, `users:read`, etc.

---

## ⚙️ Step 4: Customize Node Settings

### Gmail Trigger

**Purpose**: Monitors Gmail inbox for new unread emails

**Settings**:
- **Resource**: Message
- **Event**: On Message Received
- **Poll Interval**: 1 minute for real-time processing

**Optional Filters**:
- Filter by specific labels
- Exclude certain senders (newsletters, spam)
- Focus on specific folders

No additional config needed unless you want specific filtering rules.

### OpenAI Analysis Node

**Purpose**: Uses GPT to extract email categorization intelligently

**Key Features**:
- **Email Type**: Determines category (support, sales, marketing, etc.)
- **Priority Level**: Assesses urgency (low, normal, high, urgent)
- **Content Analysis**: Understands context and intent
- **Consistent Output**: Reliable categorization across email types

Prompt is preconfigured but feel free to modify for your specific business needs. You can add custom categories or adjust classification rules.

### Switch Node Routing

**Purpose**: Directs emails to appropriate processing paths

**Configuration**:
- Routes based on AI categorization result
- Supports multiple output paths simultaneously
- Includes fallback handling for edge cases
- Easily extensible for new categories

### Gmail Labeling Nodes

**Purpose**: Organizes emails with automatic labeling

**Benefits**:
- Creates searchable email organization
- Maintains Gmail folder structure
- Enables advanced filtering and search
- Provides visual categorization in inbox

### Slack Notification Nodes

**Purpose**: Delivers targeted team notifications

**Features**:
- Rich formatting with Slack Block Kit
- Direct email links for quick access
- Priority indicators for urgent emails
- Channel-specific routing for relevant teams
- Customizable message templates

Each category sends to appropriate channels:
- **Marketing** → `#marketing-alerts`
- **Billing** → `#finance-notifications`
- **Support** → `#support-tickets`
- **Sales** → `#sales-leads`
- **Internal** → `#internal-comms`

---

## 🔄 Workflow Overview

This workflow provides intelligent email categorization with the following flow:

1. **Gmail Trigger** monitors for new emails
2. **OpenAI Analysis** categorizes and prioritizes emails
3. **Switch Node** routes emails based on categorization
4. **Gmail Labeling** applies appropriate labels
5. **Slack Notifications** alert relevant teams

---

## 📎 Useful Links

- [n8n Docs](https://docs.n8n.io/)
- [Gmail OAuth Guide](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)
- [OpenAI Setup](https://docs.n8n.io/integrations/builtin/credentials/openai/)
- [Slack Integration](https://docs.n8n.io/integrations/builtin/credentials/slack/)
- [n8n Community Forum](https://community.n8n.io/)

---

## 🛠️ Troubleshooting

### Common Issues

1. **Gmail not triggering**
   - Verify Gmail OAuth credentials
   - Check polling interval settings
   - Ensure proper inbox permissions

2. **OpenAI analysis failures**
   - Confirm API key validity
   - Check rate limits
   - Verify model selection

3. **Slack notifications not sending**
   - Validate Slack OAuth setup
   - Check channel permissions
   - Verify bot access to channels

### Testing

Before activation:
1. Test Gmail connection with sample emails
2. Verify OpenAI categorization accuracy
3. Check Slack notification delivery
4. Test label application in Gmail

---

## ✅ Final Steps

- Activate the workflow using the **"Activate"** toggle
- Monitor initial executions for accuracy
- Adjust categorization prompts as needed
- Train team on new automated process

 
 