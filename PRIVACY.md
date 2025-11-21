# Privacy Policy — PR Guardian AI

_Last updated: 2025-11-21_

Thank you for using **PR Guardian AI**, a GitHub App designed to automate code review using AI.  
Your privacy is important to us. This document explains what data the app processes and how it is used.

---

## 1. Information We Do Not Collect
PR Guardian AI **does NOT collect, store, or sell any personal information**.

We do not:
- Store your name, email, or account information  
- Save repository contents  
- Log code or files outside GitHub  
- Track usage behavior  
- Use cookies or analytics  

We do not run a database and we do not share any information with third parties.

---

## 2. Information the App Temporarily Processes
To perform automated pull request reviews, PR Guardian AI temporarily receives:

- Pull request event payloads  
- Code diffs provided by GitHub  
- Repository metadata (name, branches, PR ID, etc.)

This data:
- Is **processed only in memory**  
- Is **never saved**  
- Is used solely to generate review comments  
- Is deleted immediately after the response is created  

---

## 3. Use of OpenAI API
To generate PR review suggestions, code diffs are temporarily sent to the OpenAI API.  
We use the API strictly for processing your request.

OpenAI does **NOT** use your data to train their models (per their API data usage policies).

---

## 4. Security
- All GitHub requests are authenticated using GitHub App installation tokens  
- Webhook signatures are validated using your app secret  
- Your private key remains on your server and is never shared  
- No data is stored or logged externally

---

## 5. Third-Party Services
The app uses:
- **GitHub API** to receive and post PR data  
- **OpenAI API** for generating code review suggestions  
- **Webhook proxy tools (Smee)** during development only

These services operate under their own privacy policies.

---

## 6. Your Control
You may at any time:
- Uninstall the app from GitHub  
- Revoke its access  
- Remove installation permissions  
- Delete your repositories or PRs

The app stops receiving data immediately after uninstallation.

---

## 7. Changes to This Policy
We may update this privacy policy to improve clarity or comply with GitHub requirements.  
All changes will be visible in this repository.

---

## 8. Contact
If you have questions or concerns, contact:

**Amir Hossein**  
GitHub: https://github.com/AmirhosseinHonardoust  
Email: _your email if you want (optional)_

---

Thank you for trusting PR Guardian AI.
