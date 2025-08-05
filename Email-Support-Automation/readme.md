


# n8n Workflow Setup Guide

This workflow integrates Gmail, OpenAI, and Slack. 

Follow this guide to install n8n, set up required credentials, and import the workflow to start automating tasks.

---

## 🔧 Prerequisites

- Node.js (if using `npx` installation)
- Docker (optional)
- Gmail account
- OpenAI API Key
- Slack workspace

---

## 🚀 Installing n8n

You can install and run n8n either using **npx** or **Docker**.

### Option 1: Install via NPX (local machine)

```bash
npx n8n
````

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

### 1. Gmail OAuth

Follow the official guide to set up Gmail credentials:

👉 [Gmail OAuth Setup Guide](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)

Once configured, add your Gmail OAuth credentials inside the **Credentials** tab in n8n.

---

### 2. OpenAI API

Create an OpenAI credential in n8n using your API key:

👉 [OpenAI Credential Setup](https://docs.n8n.io/integrations/builtin/credentials/openai/)

Ensure you’ve selected the correct model (e.g., `gpt-4`, `gpt-3.5-turbo`, etc.) in the workflow.

---

### 3. Slack OAuth

Set up Slack integration with the proper OAuth credentials:

👉 [Slack OAuth Setup](https://docs.n8n.io/integrations/builtin/credentials/slack/)

Make sure to allow appropriate scopes (`chat:write`, etc.) in your Slack App.

---

## 📥 Importing the Workflow

To import this workflow into n8n:

1. Open [http://localhost:5678](http://localhost:5678) (or your n8n instance)
2. Click on the **menu icon (☰)** in the top right
3. Choose **Import Workflow**
4. Select the `.json` workflow file from this repository
5. Click **Import**

Once imported, make sure to:

* Link the proper **credentials** to each service node
* Test each connection before activating the workflow

---

## ✅ Final Steps

* Activate the workflow using the **"Activate"** toggle in the editor
* Monitor executions via the **Executions** panel
* Adjust timing (cron node) or triggers as needed

---

## 📎 References

* [n8n Docs](https://docs.n8n.io/)
* [n8n Community Forum](https://community.n8n.io/)
* [Gmail Integration](https://docs.n8n.io/integrations/builtin/credentials/google/oauth-single-service/)
* [OpenAI Integration](https://docs.n8n.io/integrations/builtin/credentials/openai/)
* [Slack Integration](https://docs.n8n.io/integrations/builtin/credentials/slack/)


