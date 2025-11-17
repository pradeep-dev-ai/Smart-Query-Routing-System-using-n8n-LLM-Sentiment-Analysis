# Smart-Query-Routing-System-using-n8n-LLM-Sentiment-Analysis
In large organizations like Innomatics Research Labs, students from multiple branches often raise queries about their academics, access issues, certifications, or administrative concerns. Manually reviewing and routing these queries to the correct department is time-consuming and inefficient.
Objective
To build an AI-driven Query Routing System using n8n workflow automation, which:
Collects student queries from a Google Form.


Analyzes sentiment using an AI node.


Uses an LLM node to identify the correct department category.


Sends the query directly to the respective Head of Department (HOD) via email.


 Tools & Nodes Used
Google Sheet Node – To collect form responses.


Sentiment Analysis Node – To detect whether the query is Urgent or Normal.


LLM Node (Basic LLM Chain) – To classify the query into one of the available departments.


If / Switch Node – To route the query to the correct HOD.


Email Node – To send the structured query details to the department’s email address.


🏫 Available Departments (Categories)
These are the departments available in Innomatics Research Labs:
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

 Department Routing Configuration
Category
Department
Email ID
WiFi Issue
IT Support
it_support@innomatics.in
Placement
Placement Cell
placement@innomatics.in
Certification
Admin Department
admin@innomatics.in
Batch Change
Academic Coordinator
academic@innomatics.in
Technical Doubt
Trainer / Mentor
trainer@innomatics.in
LMS Access
LMS Technical Support
lms_support@innomatics.in
Payment Issue
Accounts Department
accounts@innomatics.in
Assignments / Tasks
Training Department
training@innomatics.in

