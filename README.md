# 🎓 Smart Query Routing System — Innomatics Research Labs

> An AI-powered, automated student query routing system built with **n8n**, **LLM**, and **Sentiment Analysis** to eliminate manual query handling and ensure every concern reaches the right department instantly.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Problem Statement](#-problem-statement)
- [Objective](#-objective)
- [System Architecture](#-system-architecture)
- [Tools & Nodes Used](#-tools--nodes-used)
- [Workflow Steps](#-workflow-steps)
- [Available Departments](#-available-departments)
- [Department Routing Configuration](#-department-routing-configuration)
- [Email Template](#-email-template)
- [Setup & Installation](#-setup--installation)
- [How to Use](#-how-to-use)
- [Project Structure](#-project-structure)
- [Contributing](#-contributing)

---

## 🧩 Overview

The **Smart Query Routing System** is an end-to-end automated pipeline built on **n8n workflow automation**. It intelligently collects student queries submitted via a Google Form, analyzes their urgency using Sentiment Analysis, classifies them into the correct department using a Large Language Model (LLM), and automatically dispatches a structured email to the respective Head of Department (HOD) — all without any manual intervention.

---

## ❗ Problem Statement

In large organizations like **Innomatics Research Labs**, students from multiple batches and branches raise queries daily related to academics, technical access, certifications, payments, and administrative issues.

**Challenges with manual routing:**
- Time-consuming review and forwarding process
- Queries frequently misrouted to wrong departments
- Delayed responses leading to poor student experience
- No priority differentiation between urgent and normal queries

---

## 🎯 Objective

Build an AI-driven Query Routing System using n8n that:

- ✅ Collects student queries from a **Google Form**
- ✅ Analyzes **sentiment** to detect urgency (Urgent / Normal)
- ✅ Uses an **LLM** to classify the query into the correct department
- ✅ Routes the query via **If / Switch logic** to the right HOD
- ✅ Sends a **structured email** to the department automatically

---

## 🏗️ System Architecture

```
Google Form Submission
        │
        ▼
┌─────────────────────┐
│  Google Sheets Node │  ← Reads new form responses
└────────┬────────────┘
         │
         ▼
┌────────────────────────┐
│  Sentiment Analysis    │  ← Classifies as Urgent / Normal
│  Node (AI)             │
└────────┬───────────────┘
         │
         ▼
┌────────────────────────┐
│  LLM Node              │  ← Identifies department category
│  (Basic LLM Chain)     │
└────────┬───────────────┘
         │
         ▼
┌────────────────────────┐
│  If / Switch Node      │  ← Routes based on department
└────────┬───────────────┘
         │
         ▼
┌────────────────────────┐
│  Email Node            │  ← Sends query to HOD email
└────────────────────────┘
```

---

## 🛠️ Tools & Nodes Used

| Node | Purpose |
|------|---------|
| **Google Sheets Node** | Reads student query responses submitted via Google Form |
| **Sentiment Analysis Node** | Detects urgency — classifies query as `Urgent` or `Normal` |
| **LLM Node (Basic LLM Chain)** | Classifies the query into one of the defined department categories |
| **If / Switch Node** | Routes the classified query to the correct department branch |
| **Email Node** | Sends a structured query email to the respective HOD |

---

## 🔄 Workflow Steps

### Step 1 — Trigger: Google Sheets Node
- Monitors the Google Sheet linked to the student query form
- Triggers the workflow whenever a **new row (response)** is detected
- Extracts fields: `Student Name`, `Roll Number`, `Batch`, `Query Description`, `Timestamp`

### Step 2 — Sentiment Analysis Node
- Processes the query text through an AI sentiment analysis model
- Output: `Urgent` or `Normal`
- Urgent queries are flagged in the email subject for immediate attention

### Step 3 — LLM Node (Basic LLM Chain)
- Passes the query description to the LLM with a structured prompt
- The model selects the most appropriate department from the predefined list
- Output: A single department label (e.g., `WiFi Issue`, `Payment Issue`)

**Sample LLM Prompt:**
```
You are a query classification assistant for Innomatics Research Labs.
Given the following student query, classify it into exactly one of these departments:
["Technical Doubt", "WiFi Issue", "Certification", "NASSCOM", "Batch Change",
 "Teaching Methodology", "LMS Access", "Discord Access", "Payment Issue",
 "Room Allocation", "Placement", "Resume Review", "Revoke Access",
 "Live Class Access", "Quiz Related", "Recording Video Access", "Assignments", "Tasks"]

Query: {{query_description}}

Respond with only the department name and nothing else.
```

### Step 4 — If / Switch Node
- Evaluates the LLM output (department category)
- Routes the workflow to the correct email branch based on the category

### Step 5 — Email Node
- Constructs a structured email with all relevant student details
- Sends to the department's HOD email address
- Subject line includes urgency flag: `[URGENT]` or `[NORMAL]`

---

## 🏫 Available Departments

These are the supported query categories at Innomatics Research Labs:

| # | Department Category |
|---|---|
| 1 | Technical Doubt |
| 2 | WiFi Issue |
| 3 | Certification |
| 4 | NASSCOM |
| 5 | Batch Change |
| 6 | Teaching Methodology |
| 7 | LMS Access |
| 8 | Discord Access |
| 9 | Payment Issue |
| 10 | Room Allocation |
| 11 | Placement |
| 12 | Resume Review |
| 13 | Revoke Access |
| 14 | Live Class Access |
| 15 | Quiz Related |
| 16 | Recording Video Access |
| 17 | Assignments |
| 18 | Tasks |

---

## 📬 Department Routing Configuration

| Category | Department | Email ID |
|---|---|---|
| WiFi Issue | IT Support | it_support@innomatics.in |
| Placement | Placement Cell | placement@innomatics.in |
| Certification | Admin Department | admin@innomatics.in |
| Batch Change | Academic Coordinator | academic@innomatics.in |
| Technical Doubt | Trainer / Mentor | trainer@innomatics.in |
| LMS Access | LMS Technical Support | lms_support@innomatics.in |
| Payment Issue | Accounts Department | accounts@innomatics.in |
| Assignments / Tasks | Training Department | training@innomatics.in |

> **Note:** Categories not listed above (e.g., NASSCOM, Discord Access, Resume Review, etc.) can be mapped to the most relevant department or a general support inbox. These can be extended in the Switch Node configuration.

---

## 📧 Email Template

The auto-generated email sent to each HOD follows this structure:

```
Subject: [URGENT/NORMAL] New Student Query — {Category} | {Student Name}

Dear HOD,

A new student query has been submitted and routed to your department.

────────────────────────────────────
  STUDENT QUERY DETAILS
────────────────────────────────────
  Student Name  : {Student Name}
  Roll Number   : {Roll Number}
  Batch         : {Batch}
  Submitted On  : {Timestamp}
  Priority      : URGENT / NORMAL
  Category      : {Department Category}
────────────────────────────────────

Query Description:
"{Query Text}"

────────────────────────────────────

Please review and respond to the student at the earliest.

Regards,
Smart Query Routing System
Innomatics Research Labs
```

---

## ⚙️ Setup & Installation

### Prerequisites

- [n8n](https://n8n.io/) instance (self-hosted or cloud)
- Google account with access to Google Sheets & Google Forms
- SMTP credentials for sending emails
- OpenAI (or compatible) API key for LLM and Sentiment Analysis nodes

### Steps

**1. Clone or Import the Workflow**
- Import the provided `smart_query_routing.json` workflow file into your n8n instance via **Settings → Import Workflow**.

**2. Set Up Google Form & Sheet**
- Create a Google Form with fields: `Student Name`, `Roll Number`, `Batch`, `Query Description`
- Link it to a Google Sheet (Form responses destination)
- In n8n, connect the **Google Sheets Node** to your sheet using OAuth2 credentials

**3. Configure Credentials in n8n**
- `Google Sheets OAuth2` — for reading form responses
- `OpenAI API` (or preferred LLM provider) — for LLM and Sentiment nodes
- `SMTP / Gmail` — for the Email Node

**4. Configure the Switch Node**
- Map each department label from the LLM to its corresponding email branch
- Add/update HOD email addresses per the routing table above

**5. Activate the Workflow**
- Toggle the workflow to **Active**
- n8n will now poll the Google Sheet and process new submissions automatically

---

## 🚀 How to Use

1. Share the **Google Form** link with students
2. Students submit their queries via the form
3. The n8n workflow **automatically triggers** on new submissions
4. The query is analyzed, classified, and routed — **no manual action needed**
5. The respective HOD receives a structured email instantly

---

## 📁 Project Structure

```
smart-query-routing-n8n/
│
├── workflow/
│   └── smart_query_routing.json     # n8n workflow export file
│
├── assets/
│   └── architecture_diagram.png     # System flow diagram
│
├── docs/
│   └── setup_guide.md               # Detailed setup instructions
│
└── README.md                        # Project documentation (this file)
```

---

## 🤝 Contributing

Contributions are welcome! To extend this system:

1. Fork the repository
2. Add new department categories in the Switch Node
3. Update the LLM prompt to include new department names
4. Update the routing table in this README
5. Submit a Pull Request with a clear description of changes

---

## 📄 License

This project is developed for internal use at **Innomatics Research Labs**.  
For external use or redistribution, please contact the organization.

---

<div align="center">
  Built with ❤️ using <strong>n8n</strong> · <strong>OpenAI</strong> · <strong>Google Workspace</strong><br/>
  <em>Innomatics Research Labs — Empowering Students Through Automation</em>
</div>
