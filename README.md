# Job Application Automation System (n8n)

An end-to-end AI-powered career assistant built with n8n that automates the entire job application pipeline — from job discovery and resume optimization to recruiter outreach and interview scheduling.

---

## Overview

This workflow connects multiple external services and AI agents into a single autonomous system. It handles job scraping, company research, resume tailoring, email generation, recruiter discovery, and interview scheduling with minimal manual input.

---

## Pipeline Architecture

```
Schedule Trigger
   ├── Job Scraping (Apify + LinkedIn)
   │       ├── Reddit Company Research
   │       ├── Sentiment Analysis (Gemini AI)
   │       └── Google Sheets Storage
   │
   ├── Resume Optimization Pipeline
   │       ├── Google Drive Resume Download
   │       ├── PDF → Text Conversion
   │       ├── AI Resume Rewriting (Job Description + Sentiment)
   │       ├── ATS-Optimized Resume Generation
   │       └── Google Docs / Drive Export
   │
   ├── Outreach Automation
   │       ├── Cover Letter Generation (Gemini AI)
   │       ├── Application Email Generation
   │       ├── Gmail Send
   │       └── Recruiter Discovery (Hunter.io → Google Sheets)
   │
   └── Interview Automation
           ├── Gmail Trigger (Inbound Detection)
           ├── Interview Detail Extraction (AI)
           ├── Google Calendar Event Creation
           └── Confirmation Email
```

---

## Features

**Job Discovery**
- Scrapes LinkedIn job listings via Apify
- Pulls Reddit discussions per company for context
- Runs AI-based sentiment classification (Positive / Neutral / Negative)
- Stores enriched job data in Google Sheets

**Resume Optimization**
- Downloads resume PDF from Google Drive
- Extracts text and passes it through multiple Gemini AI agents
- Rewrites and tailors resume per job description and company sentiment
- Outputs ATS-optimized resume to Google Docs and Drive

**Outreach Automation**
- Generates personalized cover letters and application emails via AI
- Sends emails automatically through Gmail
- Discovers recruiter and HR contacts using Hunter.io API
- Tracks all outreach in a Google Sheets applicant log

**Interview Scheduling**
- Monitors Gmail for incoming interview-related emails
- Extracts company name, role, date, and time using AI
- Creates Google Calendar event automatically
- Sends confirmation email to user

**Resume Upload via Webhook**
- Accepts resume submissions via webhook (base64 encoded PDF)
- Converts and uploads directly to Google Drive
- Integrates into the optimization pipeline automatically

---

## Tech Stack

| Component | Tool |
|---|---|
| Workflow Automation | n8n |
| AI Agents | Google Gemini |
| Job Scraping | Apify (LinkedIn Scraper) |
| Recruiter Discovery | Hunter.io API |
| Email | Gmail API |
| Storage | Google Drive, Google Docs, Google Sheets |
| Calendar | Google Calendar API |
| Trigger | Schedule + Webhook + Gmail |

---

## Setup

### Prerequisites

- n8n (self-hosted or cloud)
- Google account with OAuth access (Drive, Docs, Sheets, Gmail, Calendar)
- Apify account with LinkedIn Scraper enabled
- Hunter.io API key
- Google Gemini API key

### Installation

```bash
# Self-hosted via npm
npm install n8n -g
n8n start

# Or via Docker
docker run -it --rm -p 5678:5678 n8nio/n8n
```

### Import Workflow

1. Open n8n at `http://localhost:5678`
2. Click **Import Workflow**
3. Upload the provided `.json` workflow file

### Environment Variables

```env
APIFY_TOKEN=your_token
HUNTER_API_KEY=your_key
GOOGLE_GEMINI_API_KEY=your_key
```

### Configure Credentials in n8n

- Google Drive OAuth
- Google Sheets OAuth
- Google Docs OAuth
- Gmail OAuth
- Google Calendar OAuth
- Gemini API key

---

## Notes

- Do not expose API keys in the exported workflow JSON
- Ensure Gemini API quota is sufficient for concurrent agents
- Apify scraper must be active and within usage limits
- Google OAuth scopes must include Drive, Sheets, Gmail, and Calendar access

---

## Acknowledgements

Developed under the guidance of **Prof. Arpit Khandelwal**, IIT Jodhpur.

---

## License

MIT License
