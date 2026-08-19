# Nexus Talent AI — AI Resume Screener

An AI-powered career platform that scores resumes against real job listings,
maps skill gaps to learning resources, and builds exportable resumes — all in
one Flask app.

**Live demo:** https://ai-resume-screener-dl5a.onrender.com/
## Features

- **Job Dashboard** — browse listings across domains (Tech, Finance, Design,
  AI/ML, etc.), auto-sorted by company popularity and salary; pay figures are
  normalized into INR LPA regardless of source currency/format ($, £, €,
  /mo, /hr).
- **Resume Analyzer** — upload a `.pdf`, `.docx`, or `.doc` resume and get a
  match score against a job's requirements.
  - Three-layer text extraction (PyMuPDF → PyPDF2 → OCR fallback) so even
    scanned/image-based resumes work.
  - Semantic skill matching via `sentence-transformers`
    (`all-MiniLM-L6-v2`) — matches meaning, not just keywords (e.g. "JS"
    ↔ "JavaScript").
  - Score = 70% skills match + 30% structural completeness (Experience,
    Education, Projects, Skills sections).
  - Feedback breakdown: strengths, missing core skills, structural gaps.
- **Career Roadmaps** — curated learning paths per domain and per company
  (Google, Microsoft, Amazon, TCS, etc.), with links to fill missing skills.
- **Resume Builder** — fill a form, export a polished resume as PDF or DOCX.
- **Analysis Reports** — downloadable PDF report with score visuals, company
  branding, and a detailed gap analysis.

## Tech stack

| Layer | Tools |
|---|---|
| Backend | Python, Flask |
| AI/ML | `sentence-transformers`, PyTorch |
| Document processing | PyMuPDF, PyPDF2, `python-docx`, `pytesseract` (OCR), Pillow |
| PDF generation | `fpdf2` |
| Frontend | Jinja2 templates, vanilla CSS |
| Data | Flat-file JSON (`companies.json`, `domains.json`, `domains_data.json`) |
| Server | Gunicorn |

## Getting started

```bash
git clone https://github.com/chiragchauhan07/AI-Resume_Screener.git
cd AI-Resume_Screener
pip install -r requirements.txt
```

Resume OCR requires the Tesseract binary installed locally (already handled
in the Docker image below):

```bash
# Debian/Ubuntu
sudo apt-get install tesseract-ocr
```

Run it:

```bash
python app.py
```

The app serves on `http://localhost:5000`.

## Running with Docker

```bash
docker build -t nexus-talent-ai .
docker run -p 5000:5000 nexus-talent-ai
```

## Deployment

Includes a `vercel.json` for one-click deployment to Vercel, and a
`Dockerfile` for any container platform.

## Project structure

```
app.py                 # Flask app: routes, extraction, scoring, report/resume generation
templates/              # Jinja2 pages (dashboard, analysis, roadmap, resume builder, ...)
static/images/           # Company logos and UI assets
companies.json           # Job listings / company data
domains.json             # Domain metadata
domains_data.json         # Domain-specific roadmap content
Dockerfile
vercel.json
requirements.txt
```

## Documentation

See [documentation.md](documentation.md) for a deeper dive into the core
functions in `app.py` (text extraction, semantic skill matching, salary
normalization, report generation).
