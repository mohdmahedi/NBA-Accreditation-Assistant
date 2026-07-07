# NBA Accreditation Assistant 🚀

An AI-powered assistant that helps engineering faculty across India navigate the complex and time-consuming National Board of Accreditation (NBA) process — covering Self-Assessment Report (SAR) preparation, CO-PO/CO-PSO mapping, and NBA criteria interpretation.

This project was built as the **Final Capstone Project (Project 2)** during a 4-week **IBM Remote Internship** in collaboration with **Edunet Foundation** and **AICTE**.

---

## ⚠️ Important Note on Credentials

This project was originally built and tested against services on an **IBM Cloud Lite Plan** issued for the internship. That plan's API key and project credentials have since expired, so the app **will not run out of the box** — you must supply your **own** IBM Cloud / watsonx.ai credentials (API key, Project ID, and region URL) before it will work. Instructions for this are below.

---

## 📌 Problem Statement

Preparing for annual NBA accreditation traditionally takes engineering institutions months of manual, repetitive work — digging through dense manuals, interpreting compliance criteria, and manually mapping course outcomes.

**The solution:** a **Retrieval-Augmented Generation (RAG)** pipeline that grounds every answer in the official NBA manual, removing manual overhead and minimizing hallucination risk.

---

## 🌟 Core Features

- **RAG-Powered Chat Assistant** — Ask questions in plain English about SAR preparation, eligibility, or evaluation metrics. Answers are grounded in and cited from the official *NBA General Manual*.
- **NBA Criteria Dashboard** — Visual tracking of all 8 core NBA criteria across the 870-mark spectrum, with a live breakdown against the 600-mark accreditation threshold.
- **Automated CO-PO Mapper** — Generates Course Outcome → Program Outcome mapping strength and AI-driven Continuous Quality Improvement (CQI) recommendations in seconds.

---

## 🛠️ Technology Stack

| Layer | Technology |
|---|---|
| LLM Core | IBM watsonx.ai (IBM Granite models) |
| Architecture | Retrieval-Augmented Generation (RAG) |
| Knowledge Base | Vector embeddings built from the official NBA General Manual |
| Backend | Python / Flask (`app.py`, `agent_config.py`) |
| Frontend | HTML/CSS/JS (`templates/`, `static/`) |
| Deployment | Docker (`Dockerfile`, `Procfile`) |

---

## 📁 Repository Structure

```
├── knowledge_base/     # Official NBA manuals and reference documents
├── vector_store/        # Embedded indexes used by the RAG pipeline
├── static/               # Frontend assets (CSS, JS, images)
├── templates/            # Frontend HTML pages
├── utils/                # Core RAG pipeline helper scripts
├── app.py                # Main Flask application entry point
├── agent_config.py       # Configuration for the Granite LLM / watsonx connection
├── .env.example          # Template for environment variables
├── Dockerfile / Procfile # Deployment assets
└── requirements.txt
```

---

## ⚙️ Running This on Your Own System

To run this project locally with your **own** IBM Cloud account, you need three things: an **API key**, a **Project ID**, and the correct **region URL** for your watsonx.ai instance. Here's the full setup.

### 1. Clone the repository

```bash
git clone https://github.com/mohdmahedi/NBA-Accreditation-Assistant.git
cd NBA-Accreditation-Assistant
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Get your own IBM Cloud / watsonx.ai credentials

1. Sign in to [IBM Cloud](https://cloud.ibm.com) and open (or create) a **watsonx.ai project**.
2. **API Key** — go to *Manage → Access (IAM) → API keys* and generate a new key. Copy it somewhere safe; it's only shown once.
3. **Project ID** — open your watsonx.ai project, go to the **Manage** tab, and copy the **Project ID** listed there.
4. **Region URL** — watsonx.ai is region-locked, so your API calls must point at the same region your project lives in. Common endpoints:

   | Region | Endpoint URL |
   |---|---|
   | Dallas (us-south) | `https://us-south.ml.cloud.ibm.com` |
   | Frankfurt (eu-de) | `https://eu-de.ml.cloud.ibm.com` |
   | London (eu-gb) | `https://eu-gb.ml.cloud.ibm.com` |
   | Tokyo (jp-tok) | `https://jp-tok.ml.cloud.ibm.com` |
   | **Sydney (au-syd)** | `https://au-syd.ml.cloud.ibm.com` |

   If your project was provisioned in the **Sydney / Australia region**, use the `au-syd` endpoint above. You can confirm your project's region from the project's **Manage** tab in the watsonx.ai console — it's shown next to the project name.

### 4. Configure environment variables

Rename `.env.example` to `.env`:

```bash
cp .env.example .env
```

Open `.env` and replace the placeholder values with your own:

```env
IBM_CLOUD_API_KEY=your_own_api_key_here
WATSONX_PROJECT_ID=your_own_project_id_here
WATSONX_URL=https://au-syd.ml.cloud.ibm.com
```

- `IBM_CLOUD_API_KEY` → the API key you generated in step 3.
- `WATSONX_PROJECT_ID` → your watsonx.ai project's Project ID.
- `WATSONX_URL` → the endpoint matching your project's region (use the Sydney URL above if that's where your project lives, otherwise pick the matching row from the table).

> If `agent_config.py` hardcodes any of these values instead of reading from `.env`, open that file and update the same three values (API key, project ID, and region URL) directly.

### 5. Run the application

```bash
python app.py
```

Then open your browser to:

```
http://127.0.0.1:5000
```

Make sure your `.env` file (with your own API key, project ID, and region URL) is present before building/running the container.

---

## About

The objective of this project is to build an AI-powered assistant that helps faculty prepare SAR documentation, CO-PO/CO-PSO mapping, and understand NBA accreditation criteria easily and accurately.
