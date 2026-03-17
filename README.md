👇

🎯 Smart Query Routing System using n8n + LLM + Sentiment Analysis
📌 Overview

In large organizations like Innomatics Research Labs, students from multiple branches frequently raise queries related to academics, access issues, certifications, or administrative concerns.

Manually reviewing and routing these queries is:

Time-consuming

Error-prone

Not scalable

👉 This project solves that problem using AI + Automation.


.

🚀 Objective

Build an AI-driven Query Routing System using n8n workflow automation that:

Collects student queries from a Google Form

Analyzes sentiment (Urgent / Normal)

Classifies queries into the correct department using LLM

Automatically routes queries to the respective department via email


🧠 System Architecture


Google Form → Google Sheets → n8n Workflow
        ↓
Sentiment Analysis (Urgent / Normal)
        ↓
LLM Classification (Department)
        ↓
Conditional Routing (IF / Switch)
        ↓
Email Notification to HOD

🛠️ Tools & Technologies

| Tool                        | Purpose                  |
| --------------------------- | ------------------------ |
| **n8n**                     | Workflow automation      |
| **Google Forms**            | Collect student queries  |
| **Google Sheets Node**      | Store responses          |
| **Sentiment Analysis Node** | Detect urgency           |
| **LLM Node (Basic Chain)**  | Classify department      |
| **IF / Switch Node**        | Routing logic            |
| **Email Node**              | Send query to department |



🏫 Available Departments (Categories)


[
  "Technical Doubt",
  "WiFi Issue",
  "Certification",
  "NASSCOM",
  "Batch Change",
  "Teaching Methodology",
  "LMS Access",
  "Discord Access",
  "Payment Issue",
  "Room Allocation",
  "Placement",
  "Resume Review",
  "Revoke Access",
  "Live Class Access",
  "Quiz Related",
  "Recording Video Access",
  "Assignments",
  "Tasks"
]
****

**🔀 Department Routing Configuration**


| Category            | Department            | Email ID                                                      |
| ------------------- | --------------------- | ------------------------------------------------------------- |
| WiFi Issue          | IT Support            | [it_support@innomatics.in](mailto:it_support@innomatics.in)   |
| Placement           | Placement Cell        | [placement@innomatics.in](mailto:placement@innomatics.in)     |
| Certification       | Admin Department      | [admin@innomatics.in](mailto:admin@innomatics.in)             |
| Batch Change        | Academic Coordinator  | [academic@innomatics.in](mailto:academic@innomatics.in)       |
| Technical Doubt     | Trainer / Mentor      | [trainer@innomatics.in](mailto:trainer@innomatics.in)         |
| LMS Access          | LMS Technical Support | [lms_support@innomatics.in](mailto:lms_support@innomatics.in) |
| Payment Issue       | Accounts Department   | [accounts@innomatics.in](mailto:accounts@innomatics.in)       |
| Assignments / Tasks | Training Department   | [training@innomatics.in](mailto:training@innomatics.in)       |

⚙️ Workflow Steps
1. Data Collection

Students submit queries via Google Form

Responses stored in Google Sheets

2. Sentiment Analysis

AI model classifies:

Urgent

Normal






