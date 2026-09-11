# 📧 Google Sheets → Gmail Automation

A beginner-friendly n8n automation that reads tasks from Google Sheets, processes them with JavaScript, and automatically sends them by email using Gmail.

This project is the first automation in my **n8n Automation Learning Path**, designed to progress from basic workflows to advanced AI agents, RAG systems, APIs, databases, and business automation.

---

## 🚀 Workflow Architecture

```text
┌─────────────────────┐
│   Schedule Trigger  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Google Sheets    │
│     Get Rows        │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Code - JavaScript │
│                     │
│  Process Tasks      │
│  Create tasksText   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Gmail Send       │
│                     │
│    Send Tasks       │
└─────────────────────┘
```

---

## 🎯 Project Goal

The goal of this project is to automate a simple daily task-report workflow.

Instead of manually copying tasks from Google Sheets and sending them by email, n8n performs the process automatically.

### Input

Tasks are stored in Google Sheets:

| Task             |
| ---------------- |
| Study JavaScript |
| Learn Docker     |
| Build API        |
| Practice n8n     |

### Processing

n8n retrieves the rows and the JavaScript Code node converts the tasks into a single text value.

### Output

Gmail sends an email containing the tasks.

Example:

```text
Hello,

Here are your tasks:

Study JavaScript
Learn Docker
Build API
Practice n8n

Have a productive day!
```

---

## 🧩 Nodes Used

### 1. Schedule Trigger

Starts the workflow automatically according to a configured schedule.

**Purpose:**

- Start the automation automatically
- Avoid manually executing the workflow

---

### 2. Google Sheets

Reads task data from a Google Sheet.

**Purpose:**

- Retrieve tasks
- Convert spreadsheet data into n8n items

Example input:

```json
{
  "Task": "Study JavaScript"
}
```

---

### 3. Code — JavaScript

Processes all incoming items.

```javascript
const items = $input.all();

const tasksText = items
  .map((item) => item.json.Task)
  .filter((task) => task)
  .join("\n");

return [
  {
    json: {
      tasksText,
    },
  },
];
```

### What the code does

```text
$input.all()
      ↓
Get all Google Sheets items
      ↓
.map()
      ↓
Extract Task
      ↓
.filter()
      ↓
Remove empty values
      ↓
.join("\n")
      ↓
Create one text string
```

---

### 4. Gmail

Sends the final task list by email.

Example message:

```text
Hello,

Here are your tasks:

{{ $json.tasksText }}

Have a productive day!
```

---

## 🧠 Concepts Learned

This project introduces the fundamentals of n8n automation:

- Schedule Triggers
- Google Sheets integration
- Gmail integration
- n8n Items
- `$json`
- `$input.all()`
- JavaScript Code nodes
- `map()`
- `filter()`
- `join()`
- Expressions
- JSON
- Data transformation
- Workflow execution

---

## 📋 Requirements

- n8n
- Google account
- Google Sheets
- Gmail
- Basic JavaScript knowledge

This project can run with a local n8n installation or a hosted n8n instance.

---

## ⚙️ Setup

### 1. Create a Google Sheet

Create a sheet containing a column named:

```text
Task
```

Example:

```text
Task
-------------------
Study JavaScript
Learn Docker
Build API
Practice n8n
```

### 2. Import the workflow

Import:

```text
workflow.json
```

into your n8n instance.

### 3. Configure Google Sheets

Connect your Google account and select the spreadsheet containing the tasks.

### 4. Configure Gmail

Connect your Gmail account and specify the recipient.

### 5. Test the workflow

Execute the workflow manually first.

Verify that:

```text
Google Sheets
      ↓
Code
      ↓
Gmail
```

works correctly.

### 6. Activate the workflow

After successful testing, activate/publish the workflow so the Schedule Trigger can execute it automatically.

---

## 🔐 Security

**Never commit credentials or secrets to GitHub.**

Do not upload:

```text
.env
API keys
OAuth secrets
Passwords
Database credentials
Private tokens
```

The workflow should reference n8n credentials rather than exposing secret values.

---

## 📁 Project Structure

```text
01-google-sheets-gmail/
│
├── workflow.json
└── README.md
```

---

## 📈 Learning Progression

This is **Project 01** in my n8n automation roadmap.

```text
01. Google Sheets → Gmail
        ↓
02. Task Reminder
        ↓
03. JavaScript Data Processing
        ↓
04. Telegram Task Bot
        ↓
05. API Automation
        ↓
06. Lead Collection
        ↓
07. AI Email Classifier
        ↓
08. AI Task Manager
        ↓
09. AI Customer Support
        ↓
10. RAG Assistant
        ↓
11. AI Agent + Tools
        ↓
12. Multi-Agent System
        ↓
13. AI Business Automation Platform
```

---

## 🏆 Objective

The long-term objective of this repository is to document my progression from **beginner n8n workflows to advanced AI-powered automation systems**.

Each project is designed to introduce new concepts and increase the complexity of the automation architecture.

---

## 👨‍💻 Author

**Oussama Taright**

Computer Science Student | Full-Stack Developer | Instructor

GitHub: [oussamatght](https://github.com/oussamatght)

---

## ⭐ If you find this repository useful

Feel free to explore the workflows and follow the progression from simple automations to advanced AI-powered systems.
