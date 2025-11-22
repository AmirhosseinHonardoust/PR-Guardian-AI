# PR Guardian AI

### **AI-Powered Pull Request Reviewer for GitHub**

<p align="center">
  <img src="https://github.com/user-attachments/assets/cd861495-a460-43df-bfd7-4fdf3aabfdc2" width="250" alt="PR Guardian AI Logo">
</p>


<p align="center">
<!-- Badges -->
<a href="#"><img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge"></a> <a href="#"><img src="https://img.shields.io/badge/AI%20Powered-OpenAI-blue?style=for-the-badge&logo=openai"></a> <a href="#"><img src="https://img.shields.io/badge/FastAPI-Backend-009688?style=for-the-badge&logo=fastapi"></a> <a href="#"><img src="https://img.shields.io/badge/GitHub-App-black?style=for-the-badge&logo=github"></a> <a href="#"><img src="https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge"></a>
</p>

---
 
## Overview

**PR Guardian AI** is an advanced GitHub App that automatically reviews pull requests using artificial intelligence.
It reads your code diffs, finds problems, and writes professional comments inside the PR, just like a human reviewer.

This tool helps developers deliver high-quality code faster, reduces review workload, and provides consistent feedback across teams.

---

## Why PR Guardian AI?

### Features

| Feature                             | Description                                                        |
| ----------------------------------- | ------------------------------------------------------------------ |
|    AI-powered Code Review           | Automatically analyzes PR diffs using OpenAI.                      |
|    Detects Code Issues              | Finds bugs, security risks, optimization issues, unused code, etc. |
|    Comments Inside PR               | Posts human-like comments directly in the conversation.            |
|    Real-Time Webhook Processing     | Handles PR events instantly (opened, updated).                     |
|    Secure GitHub App Authentication | Uses JWT & installation token best practices.                      |
|    Works on Any Repository          | Easy installation & setup.                                         |
|    Developer Friendly               | Fully open-source & customizable.                                  |

---

## How It Works (Full Explanation)

### **1. A Pull Request is created or updated**

GitHub triggers a webhook event:
`pull_request` with action `opened`, `synchronize`, etc.

### **2. GitHub sends PR data to your backend**
 
Your backend receives it on:

```
POST /webhook
```

It contains:

* PR number
* repo information
* diff URL
* installation ID

### **3. The backend validates the signature**

Using `X-Hub-Signature-256` and your `GITHUB_WEBHOOK_SECRET`.

### **4. Backend authenticates as GitHub App**

It generates:

* JWT
* Installation Access Token

### **5. Backend fetches the PR diff**

Using:

```
https://patch-diff.githubusercontent.com/raw/.../pull/<id>.diff
```

### **6. AI analyzes the code diff**

It sends diff to OpenAI with a structured prompt:

* detect bugs
* find performance issues
* detect bad naming
* security warnings
* suggest improvements

### **7. App posts comments in the PR**

Using:

```
POST /repos/{owner}/{repo}/issues/{pr_number}/comments
```

---

## Architectural Diagram

```
 ┌──────────────┐
 │ Developer    │
 │ creates PR   │
 └──────┬───────┘
        │
        ▼
 ┌────────────────────┐
 │ GitHub Webhook     │────────────┐
 └──────┬─────────────┘            │
        │ (pull_request event)     │
        ▼                          │
 ┌───────────────────────┐         │
 │ FastAPI Backend       │         │
 │ /webhook              │         │
 └──────┬────────────────┘         │
        │                          │
        ▼                          │
 ┌─────────────────────────┐       │
 │ Verify Signature        │       │
 └──────┬──────────────────┘       │
        │                          │
        ▼                          │
 ┌─────────────────────────────┐   │
 │ Generate GitHub JWT         │   │
 │ Get Installation Token      │   │
 └──────┬──────────────────────┘   │
        │                          │
        ▼                          │
 ┌──────────────────────────────┐  │
 │ Fetch PR diff (.diff)        │  │
 └──────┬───────────────────────┘  │
        │                          │
        ▼                          │
 ┌────────────────────────────┐    │
 │ Send code to OpenAI        │    │
 │ AI Review Engine           │    │
 └──────┬─────────────────────┘    │
        │                          │
        ▼                          │
 ┌─────────────────────────────┐   │
 │ GitHub API: Post Comment    │◄──┘
 │ inside Pull Request         │
 └─────────────────────────────┘
```

---

## Installation (Developer Mode)

### 1. Clone repo

```bash
git clone https://github.com/AmirhosseinHonardoust/PR-Guardian-AI.git
cd github-ai-reviewer
```

### 2. Install requirements

```bash
pip install -r requirements.txt
```

### 3. Create `.env`

```
GITHUB_APP_ID=123456
GITHUB_PRIVATE_KEY_PATH=./private-key.pem
GITHUB_WEBHOOK_SECRET=your-secret
OPENAI_API_KEY=your-key
LOG_LEVEL=info
```

### 4. Run server

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

---

## Webhook Proxy (Local Development)

### Using Smee.io

```bash
npm install --global smee-client

smee --url https://smee.io/YOUR_ID --target http://localhost:8000/webhook
```

GitHub → App settings → Webhook URL

```
https://smee.io/YOUR_ID
```

---

## Deployment Options

| Platform                 | Status                | Difficulty |
| ------------------------ | --------------------- | ---------- |
| **Railway**              |   Recommended         |  Easy      |
| **Render**               |   Works well          |  Medium    |
| **DigitalOcean Droplet** |                       |  Medium    |
| **Heroku**               |   Requires paid Dyno  |            |
| **VPS / Bare-metal**     |   Full control        |            |

---

## Testing

Create or update a pull request →
Check PR conversation →
AI comments should appear automatically.

If not:

* Check GitHub delivery logs
* Check backend logs
* Check Smee console

---

## Contributing

Pull requests are welcome.

You can contribute:

* Better AI prompts
* Support for multiple file types
* Line-by-line review
* Security scanning
* Performance analysis

---

## License

Distributed under the **MIT License**.

---

## Credits

Built with care by **Amir Hossein Honardoust**
Helping developers write clean, optimized, and secure code using AI.

If you like this project
**Star the repo**
and
Share with others!
