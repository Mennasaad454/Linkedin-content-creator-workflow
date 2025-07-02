# LinkedIn Content Creator Workflow (n8n)

Automate LinkedIn post drafting based on topics from a Google Sheet. This n8n workflow fetches recent web content on each topic, uses AI to draft a professional post, and updates your content pipeline — saving time for creators and marketers.

---

## Overview

This workflow:
- Runs daily at a scheduled time.
- Fetches a topic marked **"To Do"** from a Google Sheet.
- Searches the web for recent, relevant content via the Tavily API.
- Uses OpenAI GPT (through LangChain) to write a professional LinkedIn post.
- Updates the Google Sheet with the drafted post and changes the topic’s status to **"Created"**.
---

## Workflow Process

### 1️⃣ Schedule Trigger  
**Node:** `Schedule Trigger`  
**Purpose:** Runs the workflow daily at **7 AM**.

---

### 2️⃣ Fetch Topic from Google Sheets  
**Node:** `Google Sheets (Read)`  
**Purpose:** Retrieves the first topic where **Status = "To Do"** from a connected Google Sheets document.

---

### 3️⃣ Search Web Content via Tavily  
**Node:** `HTTP Request` (Tavily API)  
**Purpose:** Sends a web search request using the topic as a query and fetches recent relevant results.

---

### 4️⃣ Draft Post with AI  
**Nodes:** 
- `LangChain AI Agent`
- `OpenAI Chat Model (GPT-4.1)`  

**Purpose:**  
- Summarizes the fetched content.  
- Generates a LinkedIn-ready post (under 300 words, professional, uses emojis, includes a personal AI Product Manager insight).  
- Uses a detailed system prompt to guide tone and structure.

---

### 5️⃣ Update Google Sheets  
**Node:** `Google Sheets (Write)`  
**Purpose:**  
- Updates the same row in the Google Sheet:
  - Sets **Status** to `"Created"`  
  - Inserts the AI-generated post into the **Content** column.
