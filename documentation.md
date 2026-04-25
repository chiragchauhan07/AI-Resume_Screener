# Nexus Talent AI - Project Documentation

## 🚀 Overview
**Nexus Talent AI** is a state-of-the-art career platform designed to bridge the gap between job seekers and their dream roles. It leverages Artificial Intelligence to provide deep insights into resume alignment, offers personalized career roadmaps, and helps users build professional resumes.

---

## ✨ Key Features

### 1. Intelligent Job Dashboard
- **Dynamic Browsing**: Discover opportunities across diverse domains like Technology, Finance, Design, AI/ML, and more.
- **Smart Prioritization**: Jobs are automatically sorted based on company popularity and competitive salary offerings.
- **Salary Normalization**: An internal engine converts global salary formats ($, £, €, /mo, /hr) into standardized **INR Lakhs Per Annum (LPA)** for easy comparison.

### 2. AI-Powered Resume Analyzer
- **Multi-Format Support**: Seamlessly processes `.pdf`, `.docx`, and `.doc` files.
- **Smart Text Extraction**: Uses a three-layer extraction strategy (PyMuPDF, PyPDF2, and OCR) to ensure accurate data retrieval even from complex templates.
- **Semantic Skill Matching**: Utilizes the `all-MiniLM-L6-v2` transformer model to identify skills semantically (e.g., recognizing that "JS" is "JavaScript").
- **Weighted Scoring**:
  - **70% Skills Match**: How well your expertise aligns with job requirements.
  - **30% Completeness**: Heuristic check for essential sections (Experience, Education, Projects, Skills).
- **Intelligent Feedback**: Provides a detailed breakdown of strengths, missing core skills, and structural improvements.

### 3. Career Roadmaps
- **Domain Pathways**: Expert-curated roadmaps for specific industries.
- **Company Roadmaps**: Detailed insights into top-tier companies (Google, Microsoft, Amazon, TCS, etc.), including their specific demands, common roles, and required skill stacks.
- **Learning Integration**: Suggests specific learning platforms (Coursera, Udemy, etc.) for missing skills.

### 4. Professional Resume Builder
- **Interactive Builder**: A user-friendly form to input professional details.
- **Dual Export**: Generate and download resumes in both **PDF** and **DOCX** formats instantly.

### 5. Premium Analysis Reports
- **Visual Insights**: Generates a professional PDF report featuring:
  - Alignment score progress bars.
  - Company branding (logos).
  - Executive summaries and detailed gap analysis.
  - Extracted data verification sections.

---

## 🛠️ Technical Stack

### Backend
- **Language**: Python 3.x
- **Framework**: Flask (Micro web framework)
- **Session Management**: Secure client-side sessions for storing analysis results.

### AI & Machine Learning
- **Model**: `sentence-transformers` (`all-MiniLM-L6-v2`)
- **Engine**: PyTorch (`torch`)
- **Computation**: NumPy

### Document Processing
- **PDF Extraction**: `PyMuPDF` (fitz), `PyPDF2`
- **Word Extraction**: `python-docx`
- **OCR (Optical Character Recognition)**: `pytesseract` (Tesseract OCR Engine) & `Pillow` (PIL)
- **PDF Generation**: `fpdf2`

### Frontend
- **Templating**: Jinja2
- **Structure**: HTML5
- **Styling**: Vanilla CSS3 (Modern UI with glassmorphism, gradients, and micro-animations)

### Data Management
- **Storage**: JSON-based flat-file database for high performance and portability.
- **Files**: `companies.json`, `domains.json`, `domains_data.json`.

---

## 📚 Libraries Used & Purpose

| Library | Purpose |
| :--- | :--- |
| **Flask** | Handling web routing, requests, and template rendering. |
| **sentence-transformers** | Performing semantic similarity analysis between resumes and job descriptions. |
| **PyMuPDF (fitz)** | High-fidelity text extraction and rendering PDF pages for OCR. |
| **PyPDF2** | Fallback library for PDF text parsing. |
| **python-docx** | Reading and creating Microsoft Word (.docx) documents. |
| **pytesseract** | Extracting text from image-based PDFs or scanned resumes. |
| **fpdf2** | Generating dynamic PDF reports and resumes. |
| **torch** | Supporting the transformer models for AI processing. |
| **Pillow** | Image processing library for handling OCR inputs. |
| **Werkzeug** | Providing WSGI utilities and secure filename handling. |

---

## ⚙️ Core Functions in `app.py`

- `extract_text_from_pdf_smart()`: The primary engine for retrieving text from PDFs using multiple fallback layers.
- `match_skills_intelligently()`: Uses semantic embeddings to match resume content with required job skills.
- `calculate_resume_completeness()`: Heuristic function to check for the presence of standard resume sections.
- `convert_to_inr_lpa()`: Normalizes various currency and timeframe formats into a single LPA value.
- `download_report()`: Generates the premium PDF analysis report with visual styling.
- `resume_builder()`: Handles the logic for creating and exporting user resumes.
