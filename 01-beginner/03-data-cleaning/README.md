# 🧹 Data Cleaning Pipeline — n8n

An automated **data cleaning workflow built with n8n and JavaScript Code Nodes**.

The workflow takes unclean user data containing inconsistent names, emails, spaces, uppercase/lowercase differences, and empty values, then transforms it into a clean and standardized format.

It is designed as a beginner-friendly n8n project while demonstrating important JavaScript and n8n concepts such as **Arrays, Objects, `const`, Functions, `filter()`, `map()`, `trim()`, `toLowerCase()`, `toUpperCase()`, and `$input.all()`**.

---

## 🚀 Features

- 🧹 Clean inconsistent user names
- 📧 Normalize email addresses
- ✂️ Remove unnecessary spaces with `trim()`
- 🔡 Standardize uppercase/lowercase text
- 🔀 Filter invalid or empty names
- 🔄 Transform data using `map()`
- 📦 Process multiple n8n Items
- 🧩 Work with JavaScript Arrays and Objects
- ⚡ Use n8n Code Nodes
- 🔗 Demonstrate JavaScript method chaining
- 🎯 Prepare data for future automation workflows
- 🔐 Keep credentials outside the workflow

---

## 🔄 Workflow

```text
┌─────────────────────┐
│   Manual Trigger    │
│                     │
│ Execute Workflow    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Generate Users    │
│                     │
│ Create test data    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│     Clean Data      │
│                     │
│ filter()            │
│ map()               │
│ trim()              │
│ toLowerCase()       │
│ toUpperCase()       │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│       Output        │
│                     │
│ Clean user data     │
└─────────────────────┘
```

---

## 📋 Input Data

The workflow starts with intentionally unclean data.

Example:

```json
[
  {
    "name": "oussama",
    "email": " OUSSAMA@GMAIL.COM "
  },
  {
    "name": "OUSSAMA",
    "email": "oussama@gmail.com"
  },
  {
    "name": " Oussama ",
    "email": " Oussama@gmail.com "
  },
  {
    "name": "AHMED",
    "email": " AHMED@GMAIL.COM "
  },
  {
    "name": " ahmed ",
    "email": "ahmed@gmail.com "
  },
  {
    "name": "   ",
    "email": "test@gmail.com"
  }
]
```

The data intentionally contains:

- Leading spaces
- Trailing spaces
- Uppercase letters
- Lowercase letters
- Mixed capitalization
- Empty names
- Inconsistent email formatting

---

## 🧹 Data Cleaning Process

The workflow performs several cleaning operations.

### 1. Get all input Items

n8n provides the incoming Items through:

```javascript
const items = $input.all();
```

This returns all Items received by the Code Node.

---

### 2. Remove empty names

The workflow uses:

```javascript
.filter(item => item.json.name.trim() !== "")
```

This removes Items where the name is empty or contains only spaces.

For example:

```text
"oussama"   → Keep ✅

"AHMED"     → Keep ✅

"   "       → Remove ❌
```

### What is `filter()`?

`filter()` is used to **select which elements should remain in an Array**.

In simple terms:

```text
filter() = Who should stay?
```

---

### 3. Clean the name

The workflow uses:

```javascript
const name = item.json.name.trim().toLowerCase();
```

For example:

```text
"  OUSSAMA  "
```

becomes:

```text
"oussama"
```

The first letter is then converted to uppercase:

```javascript
const cleanName = name.charAt(0).toUpperCase() + name.slice(1);
```

Result:

```text
"Oussama"
```

---

### 4. Clean the email

The email is normalized using:

```javascript
const cleanEmail = item.json.email.trim().toLowerCase();
```

Example:

```text
" OUSSAMA@GMAIL.COM "
```

becomes:

```text
"oussama@gmail.com"
```

---

### 5. Transform every Item with `map()`

The workflow uses:

```javascript
.map(item => {
```

`map()` processes every element and returns a new transformed element.

In simple terms:

```text
map() = How should each element change?
```

Example:

```text
oussama     → Oussama
OUSSAMA     → Oussama
 Oussama    → Oussama
AHMED       → Ahmed
 ahmed      → Ahmed
```

---

## 🧠 `filter()` vs `map()`

This project demonstrates the important difference between the two.

### `filter()`

Used to decide which elements remain:

```javascript
const result = users.filter((user) => user.age >= 18);
```

Meaning:

```text
Keep users whose age is 18 or higher.
```

---

### `map()`

Used to transform every element:

```javascript
const result = users.map((user) => {
  return user.name.toUpperCase();
});
```

Meaning:

```text
Transform every user's name into uppercase.
```

### Easy rule

```text
filter() → SELECT

map() → TRANSFORM
```

---

## 💻 Main Code

The main cleaning Code Node contains:

```javascript
const cleanedUsers = $input
  .all()
  .filter((item) => item.json.name.trim() !== "")
  .map((item) => {
    const name = item.json.name.trim().toLowerCase();

    const cleanName = name.charAt(0).toUpperCase() + name.slice(1);

    const cleanEmail = item.json.email.trim().toLowerCase();

    return {
      json: {
        name: cleanName,
        email: cleanEmail,
      },
    };
  });

return cleanedUsers;
```

---

## 📤 Output

After processing the input, the workflow produces clean data:

```json
[
  {
    "name": "Oussama",
    "email": "oussama@gmail.com"
  },
  {
    "name": "Oussama",
    "email": "oussama@gmail.com"
  },
  {
    "name": "Oussama",
    "email": "oussama@gmail.com"
  },
  {
    "name": "Ahmed",
    "email": "ahmed@gmail.com"
  },
  {
    "name": "Ahmed",
    "email": "ahmed@gmail.com"
  }
]
```

The empty-name Item is removed.

---

## 🧩 JavaScript Concepts Demonstrated

This workflow introduces several important JavaScript concepts.

### `const`

Used to create variables:

```javascript
const name = "oussama";
```

---

### Arrays

Used to store multiple values:

```javascript
const names = ["oussama", "ahmed", "ali"];
```

---

### Objects

Used to represent structured data:

```javascript
const user = {
  name: "Oussama",
  email: "oussama@gmail.com",
};
```

---

### Functions

Used to organize reusable logic:

```javascript
function cleanName(name) {
  return name.trim();
}
```

---

### `filter()`

Selects elements:

```javascript
users.filter(...)
```

---

### `map()`

Transforms elements:

```javascript
users.map(...)
```

---

### `trim()`

Removes spaces at the beginning and end:

```javascript
name.trim();
```

---

### `toLowerCase()`

Converts text to lowercase:

```javascript
email.toLowerCase();
```

---

### `toUpperCase()`

Converts text to uppercase:

```javascript
name.toUpperCase();
```

---

## 🔗 Method Chaining

One of the main JavaScript concepts demonstrated by this project is **method chaining**.

Instead of:

```javascript
const users = $input.all();

const filteredUsers = users.filter(...);

const cleanedUsers = filteredUsers.map(...);

return cleanedUsers;
```

we can write:

```javascript
const cleanedUsers = $input.all()
  .filter(...)
  .map(...);

return cleanedUsers;
```

The workflow processes the data step by step:

```text
$input.all()
     ↓
filter()
     ↓
map()
     ↓
cleanedUsers
     ↓
return
```

---

## 🧪 Example Scenarios

### Unclean name

```text
Input:
"  OUSSAMA  "

Output:
"Oussama"
```

---

### Uppercase name

```text
Input:
"AHMED"

Output:
"Ahmed"
```

---

### Mixed capitalization

```text
Input:
"oUsSaMa"

Output:
"Oussama"
```

---

### Empty name

```text
Input:
"   "

Output:
Removed ❌
```

---

### Unclean email

```text
Input:
" OUSSAMA@GMAIL.COM "

Output:
"oussama@gmail.com"
```

---

## 🛠️ Setup

### 1. Import the workflow

Import the provided `.json` workflow into your n8n instance.

---

### 2. Execute the workflow

Click:

```text
Execute Workflow
```

The Manual Trigger will start the workflow.

---

### 3. Inspect the Code Node

Open the **Clean Data** Code Node and inspect:

- Input
- JavaScript code
- Output

You should see the original unclean data in the Input section and the standardized data in the Output section.

---

## 📁 Project Structure

```text
data-cleaning-n8n/

│
├── README.md
│
└── data-cleaning.json
```

---

## 🔮 Future Improvements

This workflow can be extended with:

- 📊 Google Sheets as the input source
- 📧 Gmail data collection
- 🗄️ PostgreSQL integration
- 🍃 MongoDB integration
- 🔍 Email validation
- 📱 Phone number normalization
- 🌍 Country and city normalization
- 🧹 Duplicate user detection
- 🚨 Invalid data detection
- 📝 Data validation
- 🔀 Conditional processing with IF
- 📊 Generate data-cleaning reports
- 🗃️ Store cleaned data in a database
- 🔔 Notify an administrator about invalid records
- 🤖 AI-powered data classification

---

## 🏗️ Technologies

- **n8n** — Workflow automation
- **JavaScript** — Data processing
- **n8n Code Node** — Custom JavaScript execution
- **Arrays** — Collection processing
- **Objects** — Structured data
- **`filter()`** — Data selection
- **`map()`** — Data transformation

---

## 🎯 Learning Objectives

This project was created to practice:

```text
JavaScript Basics
       ↓
Arrays & Objects
       ↓
Functions
       ↓
filter()
       ↓
map()
       ↓
String Manipulation
       ↓
n8n Code Node
       ↓
Data Cleaning
       ↓
Automation
```

The project demonstrates how JavaScript can be used inside n8n to process and prepare data before sending it to another service, database, API, or automation step.

---

## 💡 Why This Project?

Real-world automation workflows rarely receive perfectly formatted data.

User input can contain:

```text
Extra spaces
Wrong capitalization
Empty values
Inconsistent formatting
Duplicate information
Invalid data
```

Data cleaning is therefore an important step before processing information further.

This project provides a simple introduction to building **data-processing pipelines with JavaScript and n8n**.

---

## 📄 License

This project is provided for learning and automation purposes.

Feel free to modify and adapt it for your own n8n workflows.
