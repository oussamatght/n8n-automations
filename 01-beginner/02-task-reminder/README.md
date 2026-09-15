# ⏰ Smart Task Reminder — n8n

An automated **task reminder workflow built with n8n, Google Sheets, and Gmail**.

The workflow runs automatically every day, reads tasks from Google Sheets, checks their deadlines and status, and sends an email reminder when a task is due or overdue.

It is designed as a simple beginner-friendly automation while demonstrating important n8n concepts such as **Schedule Trigger, Google Sheets, IF conditions, DateTime expressions, Gmail, and data updates**.

---

## 🚀 Features

- ⏰ Automatic daily execution
- 📊 Read tasks from Google Sheets
- 📅 Compare task deadlines with the current date
- 🔀 Use conditional logic with IF
- 📧 Send automatic Gmail reminders
- 🎯 Support task priorities
- ✅ Track task status
- 🔔 Prevent duplicate reminders
- 📝 Update the spreadsheet after a reminder is sent
- 🔐 Keep credentials outside the workflow JSON

---

## 🔄 Workflow

```text
┌─────────────────────┐
│   Schedule Trigger  │
│      Every Day      │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Google Sheets    │
│     Get Tasks       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│        IF           │
│                     │
│ Status = pending    │
│ Reminded = no       │
│ Deadline <= Today   │
└──────────┬──────────┘
           │
          YES
           │
           ▼
┌─────────────────────┐
│        Gmail        │
│   Send Reminder     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│    Google Sheets    │
│  Reminded = yes     │
└─────────────────────┘
```

---

## 📋 Google Sheets Structure

Create a Google Sheet with the following columns:

| Task   | Deadline   | Email                                   | Status  | Priority | Reminded |
| ------ | ---------- | --------------------------------------- | ------- | -------- | -------- |
| Study  | 2026-09-12 | [your@email.com](mailto:your@email.com) | pending | High     | no       |
| Docker | 2026-09-15 | [your@email.com](mailto:your@email.com) | pending | Medium   | no       |

### Column descriptions

**Task**
The name of the task.

**Deadline**
The task deadline in:

```text
YYYY-MM-DD
```

Example:

```text
2026-09-15
```

**Email**
The email address that should receive the reminder.

**Status**
Recommended values:

```text
pending
completed
cancelled
```

**Priority**

```text
High
Medium
Low
```

**Reminded**

```text
yes
no
```

This prevents the workflow from repeatedly sending the same reminder.

---

## 🧠 How the Deadline Check Works

The workflow compares the deadline from Google Sheets with the current date.

The main expression is:

```javascript
{
  {
    DateTime.fromISO($json.Deadline).startOf("day") <= $now.startOf("day");
  }
}
```

This means:

> If the task deadline is today or has already passed, the task is eligible for a reminder.

The workflow also checks:

```text
Status = pending
```

and:

```text
Reminded = no
```

All conditions must be satisfied before the email is sent.

---

## 📧 Example Reminder

The Gmail node sends a message similar to:

```text
Hello,

This is your task reminder.

Task: Docker

Due date: 2026-09-15

Priority: Medium

Status: pending

Please complete this task as soon as possible.

Best regards,
n8n
```

---

## 🛠️ Setup

### 1. Import the workflow

Import the provided `.json` workflow into your n8n instance.

### 2. Configure Google Sheets

Open the **Google Sheets** nodes and configure:

- Google Sheets credentials
- Spreadsheet
- Worksheet

Replace the placeholder values:

```text
YOUR_GOOGLE_SHEET_ID
YOUR_SHEET_NAME
```

with your own values inside n8n.

### 3. Configure Gmail

Open the **Send Reminder** node and connect your Gmail credential.

The recipient is taken directly from the Google Sheets `Email` column:

```javascript
{
  {
    $json.Email;
  }
}
```

### 4. Test the workflow

Before activating the automation:

1. Add a test task.
2. Set its deadline to today.
3. Set `Status` to `pending`.
4. Set `Reminded` to `no`.
5. Run the workflow manually.
6. Verify that the email arrives.
7. Verify that `Reminded` changes to `yes`.

### 5. Activate

Once everything works correctly, activate the workflow.

The Schedule Trigger will then run automatically.

---

## 🔐 Security

**Never commit credentials or secrets to GitHub.**

This workflow intentionally does not contain:

- Google OAuth secrets
- Gmail passwords
- API keys
- Access tokens
- n8n instance identifiers
- Personal spreadsheet URLs
- Personal credential IDs

Keep authentication inside **n8n Credentials**.

For public repositories, use placeholders such as:

```text
YOUR_GOOGLE_SHEET_ID
YOUR_SHEET_NAME
```

---

## ⚙️ Customization

### Change the execution time

The default schedule runs at:

```text
09:00
```

You can change the Schedule Trigger to run:

- Every morning
- Every hour
- Every weekday
- At a specific time
- Using a custom cron expression

---

## 📅 Reminder Behavior

The default workflow sends a reminder when:

```text
Deadline <= Today
AND
Status = pending
AND
Reminded = no
```

After successfully sending the email:

```text
Reminded → yes
```

This helps prevent duplicate reminders.

---

## 💡 Future Improvements

The workflow can be extended with:

- 🔔 Reminders one day before the deadline
- 🚨 Different messages for overdue tasks
- 🎨 HTML email templates
- 📱 Telegram notifications
- 💬 WhatsApp notifications
- 📊 Weekly task summaries
- 📈 Productivity reports
- 🗓️ Google Calendar integration
- 🔁 Automatic recurring tasks
- ⏳ Multiple reminder intervals
- 👥 Reminders for multiple users
- 🚨 High-priority task alerts
- 📊 Dashboard and statistics
- 🛡️ Error handling and retry workflows

---

## 🧪 Example Scenarios

### Task due today

```text
Task: Docker
Deadline: 2026-09-15
Status: pending
Reminded: no
```

Result:

```text
📧 Reminder sent
Reminded → yes
```

### Task already completed

```text
Status: completed
```

Result:

```text
🚫 No reminder
```

### Reminder already sent

```text
Reminded: yes
```

Result:

```text
🚫 No duplicate email
```

### Future task

```text
Deadline: 2026-09-20
```

Result:

```text
🚫 No reminder yet
```

---

## 🏗️ Technologies

- **n8n** — Workflow automation
- **Google Sheets** — Task database
- **Gmail** — Email notifications
- **DateTime Expressions** — Deadline calculations

---

## 📁 Project Structure

```text
task-reminder/
│
├── README.md
│
└── task-reminder.json
```

---

## ⭐ Why This Project?

This project is a practical example of combining different automation concepts into one workflow.

It demonstrates:

```text
Triggers
   ↓
Data Retrieval
   ↓
Date Processing
   ↓
Conditions
   ↓
Notifications
   ↓
Data Updates
```

It can also serve as a starting point for more advanced personal productivity and business automation workflows.

---

## 📄 License

This project is provided for learning and automation purposes.

Feel free to modify and adapt it for your own n8n workflows.
