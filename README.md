# EmailSummarizer

EmailSummarizer is a Node.js-based application that securely connects to a user's Gmail account, retrieves recent email messages, and utilizes a locally hosted large language model (LLM) via Ollama to perform automated classification and summarization. This program was written as part of an academic course.

---

## Prerequisites

### 1. Node.js & npm

Install Node.js (v18+ recommended):
[https://nodejs.org/](https://nodejs.org/)

Install dependencies:

```bash
npm install
```

---

### 2. Set up Gmail API via Google Cloud Console

#### a. Create a Google Cloud Project

1. Go to [Google Cloud Console](https://console.cloud.google.com/).
2. Create a new project.

#### b. Enable Gmail API

1. In your new project, go to **APIs & Services > Library**.
2. Search for "Gmail API" and enable it.

#### c. Configure OAuth Consent Screen

1. Go to **APIs & Services > OAuth consent screen**.
2. Choose "External" and fill in required info.
3. You can skip the scopes section for development, but it’s recommended to **add the necessary scopes** explicitly.

##### Required Scopes

For read-only access to Gmail, add the following OAuth scope:

```
https://www.googleapis.com/auth/gmail.readonly
```

This allows your app to **read but not modify** the user's emails. It’s the minimum required for this project.

#### d. Create OAuth Credentials

1. Go to **APIs & Services > Credentials**.
2. Click "Create Credentials" > **OAuth Client ID**.
3. Choose "Desktop App" as the application type.
4. Download the `credentials.json` file and place it in your project root.

When you run the project, it will launch a browser to complete the authentication and save your token to `token.json`.

---

### 3. Run Ollama Locally

Install Ollama from [https://ollama.com/download](https://ollama.com/download)

Then start the desired model:

```bash
ollama run mistral
```

You can also use other models like `llama3`, `gemma`, etc., by pulling and running:

```bash
ollama pull llama3
ollama run llama3
```

if using another model rather than mistral, then make necessary changes to the classifier.js and summarizer.js files as per langchain documentation.

---

## How to Use

Once all setup is complete:

### 1. Clone the repo

```bash
git clone https://github.com/Faheem12005/EmailSummarizer.git
cd EmailSummarizer
```

### 2. Set environment variables

Create a `.env` file (if needed, for future customization). Currently, local models like Ollama don't require API keys.

### 3. Run the App

```bash
node index.js
```

This will:

* Authenticate with Gmail
* Fetch the 25 most recent emails
* Classify and summarize them in parallel using LangChain and Mistral

### Output Example

```bash
From: example@example.com
Subject: Welcome to the Hackathon!
Summary: Invitation to join an upcoming hackathon including agenda and registration details.
Classification:
{
  "type": "opportunities",
  "priority": "high",
  "reason": "A competitive event offering learning and exposure."
}
```

---


## Future Improvements

* Add vector DB support (e.g., Chroma, Weaviate) to store summaries.
* UI dashboard for visualizing email summaries.
* Labeling or automated response suggestions.
* Daily email digest generation and notifications.

---

## License

This project is for educational and personal use only. Use responsibly and comply with Gmail's API usage policies.

---

