🚀 Marketing Team AI Agent

An AI-powered automated marketing workflow built using n8n, OpenAI, Hugging Face, Twitter API, and Google Workspace.
It autonomously creates social media content, designs matching images, publishes posts, and sends analytical reports — all without human intervention.

🧠 Overview

The Marketing Team AI Agent automates the entire content marketing cycle:

Generates creative post content with OpenAI

Designs branded visuals with Hugging Face Diffusion

Publishes posts automatically to Twitter/X

Logs every post’s data in Google Sheets

Prepares weekly Google Docs reports

Emails performance reports to the marketing manager

This project demonstrates a fully autonomous digital marketing pipeline — perfect for teams aiming for productivity, creativity, and automation excellence.

🧰 Tech Stack
Category	Tools / Services
Automation Engine	n8n (Self-Hosted)

Text Generation	OpenAI GPT-4o-mini

Image Generation	Hugging Face Diffusion

Social Posting	Twitter API v2

Storage & Reporting	Google Sheets, Docs, Gmail

Monitoring	Google Drive Logs + n8n Error Workflow

🏗️ System Architecture
┌────────────┐  Trigger (Cron/Webhook)   ┌──────────────┐   Prompt   ┌──────────┐
│  n8n Flow  │ ─────────────────────────▶│   OpenAI     │──────────▶ │  Hugging │
│  Orchestrator │                         │ Text Engine  │           │  Face    │
└──────┬──────┘                           └─────┬────────┘           └─────┬────┘
       │                                       │                        │
       ▼                                       ▼                        ▼
┌────────────┐   Publish   ┌────────────┐   Log   ┌─────────────┐   Email  ┌──────────┐
│  Twitter   │◀────────────│ Google Docs│◀────────│ Google Sheets│────────▶│  Gmail   │
└────────────┘              └────────────┘          └─────────────┘         └──────────┘

⚙️ Setup Guide
1️⃣ Prerequisites

Node.js & Docker installed (for self-hosting n8n)

n8n instance with HTTPS access

Google Cloud Service Account (for Sheets, Docs, Gmail)

Developer accounts for OpenAI, Hugging Face, and Twitter API

2️⃣ Environment Variables

Create a .env file in your root directory:

TIMEZONE=Asia/Kolkata
N8N_WEBHOOK_URL=https://your-n8n-instance/webhook

OPENAI_API_KEY=sk-xxxx
OPENAI_MODEL=gpt-4o-mini

HF_API_TOKEN=hf_xxxxx
HF_IMAGE_MODEL=stabilityai/stable-diffusion-2-1

TWITTER_API_KEY=xxxx
TWITTER_API_SECRET=xxxx
TWITTER_ACCESS_TOKEN=xxxx
TWITTER_ACCESS_SECRET=xxxx

GOOGLE_APPLICATION_CREDENTIALS=/workspace/keys/google-sa.json
MANAGER_EMAIL=manager@example.com
REPORT_SHEET_ID=your_google_sheet_id
REPORT_DOC_TEMPLATE_ID=your_google_doc_template_id

3️⃣ Workflow Setup in n8n
🧩 Workflow A: Content_Generate_Post

Trigger (Cron twice daily at 10:00 & 17:00 IST)

Load brand.json for tone and hashtags

Generate 3 variants using OpenAI prompts

Create an image using Hugging Face

Publish to Twitter with image + hashtags

Append post details (date, text, link) to Google Sheet

🧩 Workflow B: Reporting_Weekly

Trigger every Friday 18:00 IST

Fetch last week’s post stats from Twitter

Compile results in a Google Doc template

Email report to the manager via Gmail

🧩 Workflow C: Monitor_And_Retry

Catch node errors automatically

Retry failed tasks with exponential backoff

Log errors to Google Sheets

🧭 Step-by-Step Automation Flow
Step	Task	Tool
1	Trigger via Cron/Webhook	n8n
2	Generate post content	OpenAI
3	Create matching image	Hugging Face
4	Post to Twitter	Twitter API
5	Log post data	Google Sheets
6	Generate weekly report	Google Docs
7	Email report to manager	Gmail
🗂️ Project Structure
marketing-team-ai-agent/
├─ /n8n-exports/             # JSON exports of workflows
├─ /prompts/                 # Custom prompt templates
│  ├─ post_short.md
│  ├─ post_long.md
│  └─ problem_solution.md
├─ /brand/
│  └─ brand.json             # Branding tone, hashtags, etc.
├─ /templates/
│  └─ report_template.md     # Weekly report template
├─ .env.example
├─ LICENSE
└─ README.md

🧠 Example Prompt (Short Post)
You are a senior content strategist for {{brand_name}}.
Write a short, engaging post (max 280 characters) with 1 emoji and 2 hashtags.
Tone: {{tone}}
Topic: {{topic}}
Output: plain text only.

🧾 Logging Example (Google Sheets)
Timestamp	Campaign	Platform	Likes	Retweets	Comments	Post Link
2025-11-07 10:00	AI Awareness	Twitter	156	32	10	View Post
📈 Reporting Example

Every Friday, a Google Doc report is generated and emailed automatically with metrics like:

Total posts published

Engagement summary (likes, comments, retweets)

Top-performing post

Visual summary graph (auto-inserted from Sheets)

🧩 Troubleshooting
Issue	Cause	Fix
“Workflow cannot execute”	Missing credentials	Reconnect in n8n Credentials
“Binary file 'data' missing”	No image in node	Add “Move Binary Data” before Drive upload
API Errors (Twitter/Google)	Token expired	Refresh OAuth credentials
Empty posts	Prompt error	Add guardrails and character limit
🔄 Extending the Agent

✅ Add LinkedIn publishing (via LinkedIn API + n8n HTTP node)
✅ Add Slack alerts for failed posts
✅ Integrate Canva API for branded templates
✅ Add analytics dashboard using Google Data Studio

📣 Why This Project Matters

🚀 Eliminates manual posting and content prep

📊 Centralizes reporting and analysis

🧠 Uses AI to maintain brand consistency

💼 Demonstrates professional-grade workflow automation skills

🔗 Perfect addition to a Data Science or AI portfolio
