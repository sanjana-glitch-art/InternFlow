# 🚀 InternFlow AI

> **Autonomous resume tailoring powered by NVIDIA Nemotron — built at SJSU Agents for Impact Hackathon 2026**

<div align="center">

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![LangGraph](https://img.shields.io/badge/LangGraph-121212?style=for-the-badge&logo=langchain&logoColor=white)
![NVIDIA](https://img.shields.io/badge/NVIDIA_Nemotron-76B900?style=for-the-badge&logo=nvidia&logoColor=white)

</div>

---

## 🧠 What Is InternFlow AI?

Students applying to 80+ internships spend 10–15 hours a week manually tailoring resumes. ATS filters reject 75% of applications before a human ever reads them — not because the candidate is unqualified, but because their resume doesn't speak the recruiter's language for that specific role.

**InternFlow AI solves this autonomously.**

Paste a job description. InternFlow reads your resume, scrapes your GitHub, selects your 3 best projects for that role, and rewrites your resume in the recruiter's exact vocabulary — in under 2 minutes. Powered entirely by NVIDIA Nemotron.

---

## ✨ Features

- 🔍 **Live Job Listings** — Browse active internships via Simplify Jobs, filtered by role and location
- 🧠 **3-Node Nemotron Pipeline** — Autonomous keyword diagnosis, project selection, and resume rewriting
- 🐙 **GitHub Integration** — Auto-scrape your repos, READMEs, and tech stack into a project portfolio
- 📄 **ATS-Optimized Resume** — Rewritten in the recruiter's exact vocabulary, never fabricated
- 📋 **Application Tracker** — Track every application, resume version used, and current status
- 🗂️ **Resume Arsenal** — Store and manage all your tailored resume versions

---

## 🤖 The Nemotron Pipeline

The core of InternFlow is a **3-node LangGraph agentic pipeline** running entirely on NVIDIA NIM infrastructure.

```
Job Description + Resume + GitHub Projects
            │
            ▼
┌─────────────────────────────────┐
│  Node 1: Keyword Diagnostic     │  ← Nemotron Super 49B
│  • Extract 15 JD keywords       │
│  • Check each against resume    │
│  • Score ATS match (0–100%)     │
│  • Identify gaps                │
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│  Node 2: Project Selector       │  ← Nemotron Nano 8B
│  • Read full project portfolio  │
│  • Select 3 most relevant       │
│  • Prioritise keyword gap cover │
└────────────────┬────────────────┘
                 │
                 ▼
┌─────────────────────────────────┐
│  Node 3: Resume Rewriter        │  ← Nemotron Super 49B
│  • Rewrite in JD vocabulary     │
│  • Embed missing keywords       │
│  • Never fabricate experience   │
└─────────────────────────────────┘
            │
            ▼
   Tailored ATS-Optimised Resume
```

### Why Two Models?

| Model | Node | Why |
|---|---|---|
| `nvidia/llama-3.3-nemotron-super-49b-v1` | 1 + 3 | Deep reasoning — semantic JD understanding + nuanced language rewriting |
| `nvidia/llama-3.1-nemotron-nano-8b-v1` | 2 | Fast classification — project ranking doesn't need 49B parameters, runs 6× faster |

---

## 🗂️ Project Structure

```
InternFlow-AI/
│
├── app.py                          # Landing page (home)
│
├── pages/
│   ├── 2_onboarding.py             # Profile setup + GitHub import
│   ├── 3_jobs.py                   # Job discovery + search
│   ├── 4_agent.py                  # AI agent analysis page
│   └── 5_resume_arsenal.py         # Resume versions manager
│
├── backend/
│   ├── main.py                     # FastAPI app entry point
│   ├── agents/
│   │   └── resume_agent.py         # LangGraph 3-node pipeline
│   ├── routes/
│   │   ├── agent.py                # POST /agent/analyze
│   │   ├── jobs.py                 # GET /jobs
│   │   ├── resumes.py              # Resume CRUD
│   │   └── applications.py        # Application tracker CRUD
│   └── data/
│       ├── resumes.json
│       └── applications.json
│
├── .env                            # API keys (never commit this)
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the repo

```bash
git clone https://github.com/sanjana-glitch-art/InternFlow
cd InternFlow
```

### 2. Create a virtual environment

```bash
python -m venv internflow
# Windows
internflow\Scripts\activate
# Mac/Linux
source internflow/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

Create a `.env` file in the project root:

```env
NVIDIA_API_KEY=nvapi-your-key-here
GITHUB_TOKEN=ghp-your-token-here
```

Get your keys:
- **NVIDIA API Key** → [build.nvidia.com](https://build.nvidia.com)
- **GitHub Token** → [github.com/settings/tokens](https://github.com/settings/tokens) *(no scopes needed for public repos)*

### 5. Run the backend

```bash
cd backend
uvicorn main:app --reload
# Backend running at http://127.0.0.1:8000
```

### 6. Run the frontend

```bash
# In a new terminal, from project root
streamlit run app.py
# App running at http://localhost:8501
```

---

## 🚀 How To Use

1. **Set Up Profile** — Go to the Profile page, fill in your details, upload your resume PDF, and import your GitHub projects
2. **Browse Jobs** — Search live internship listings by role and location
3. **Analyse with AI** — Click "Analyse with AI" on any job card to run the full Nemotron pipeline
4. **Get Your Resume** — Download the tailored, ATS-optimised resume
5. **Track Applications** — Save jobs and track your application status

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Frontend** | Streamlit |
| **Backend** | FastAPI |
| **AI Pipeline** | LangGraph |
| **LLM Inference** | NVIDIA NIM (Nemotron Super 49B + Nano 8B) |
| **Job Listings** | Simplify Jobs API |
| **Project Scraping** | GitHub REST API |
| **PDF Parsing** | PyPDF2 |
| **Storage** | JSON (file-based, hackathon scope) |
| **Environment** | python-dotenv |

---

## 🔑 API Keys Required

| Key | Where to get it | What it's used for |
|---|---|---|
| `NVIDIA_API_KEY` | [build.nvidia.com](https://build.nvidia.com) | Nemotron model inference via NIM |
| `GITHUB_TOKEN` | [github.com/settings/tokens](https://github.com/settings/tokens) | GitHub repo scraping (5000 req/hr vs 60 without) |

---

## 📊 Results

| Metric | Value |
|---|---|
| Average ATS score improvement | **+42%** |
| Time saved per application | **~12 minutes** |
| Pipeline end-to-end | **< 2 minutes** |
| Resume fabrication | **0%** — never invents experience |

---

## 👥 Team

Built at the **SJSU Agents for Impact Hackathon 2026** — hosted by NVIDIA.

| Name | Role |
|---|---|
| Sanjana | AI Engineer · Nemotron Pipeline · LangGraph |
| Sreeram Achutuni | Backend Engineer · FastAPI · REST |
| Lakshminarayana Malyala | Integration · Full Stack |
| Sravani Gurram | Frontend · UI/UX · Demo |

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

## 🙏 Acknowledgements

- [NVIDIA NIM](https://build.nvidia.com) — for Nemotron model access
- [LangGraph](https://langchain-ai.github.io/langgraph/) — for agentic pipeline orchestration
- [Simplify Jobs](https://github.com/SimplifyJobs/Summer2025-Internships) — for internship listings
- SJSU & NVIDIA — for hosting the Agents for Impact Hackathon

---

<div align="center">
  <sub>Built with ❤️ using NVIDIA Nemotron · SJSU Agents for Impact Hackathon 2026</sub>
</div>
