# 🎯 AI-Based Paper Scanner & OMR Evaluation System

A production-grade MVP for scanning and auto-evaluating OMR (Optical Mark Recognition) answer sheets for schools, colleges, universities, and coaching institutes.

![License](https://img.shields.io/badge/license-MIT-blue) ![Node](https://img.shields.io/badge/node-18%2B-green) ![Python](https://img.shields.io/badge/python-3.10%2B-yellow) ![React](https://img.shields.io/badge/react-18-cyan)

## 🌟 Features

### ✅ Implemented (v1 MVP)
- **OMR Scanning Engine** — OpenCV-based, with perspective correction, bubble detection, and confidence scoring
- **Multi-input support** — Webcam, mobile camera (PWA), JPG/PNG/PDF upload
- **MCQ Evaluation** — Single/multiple correct answers, negative marking, partial credit, skip handling
- **Admin Panel** — Exam creation, answer key management, bulk upload, user management
- **Student Results** — Instant scoring, subject-wise analysis, downloadable scorecard
- **Analytics Dashboard** — Topper list, pass %, difficulty analysis, accuracy charts
- **Security** — JWT auth, role-based access (Admin/Evaluator/Student), QR validation, audit logs, bcrypt password hashing
- **Mobile PWA** — Installable, offline-capable, real-time camera capture
- **Export** — PDF scorecard, CSV/Excel results

### 🗺️ Roadmap (v2+)
- Face verification during exam
- AI descriptive answer grading (LLM-based)
- WhatsApp/SMS gateway
- Hall ticket generator
- Native Android/iOS apps

---

## 📂 Project Structure

```
omr-system/
├── backend/              # Node.js + Express API
├── omr-engine/           # Python + OpenCV microservice
├── frontend/             # React + Vite + Tailwind (PWA)
├── templates/            # Printable OMR sheet templates
├── samples/              # Sample scanned sheets
├── docs/                 # API docs, DB schema, deployment
├── docker-compose.yml    # One-command deployment
└── README.md
```

---

## 🚀 Quick Start

### Option A: Docker (Recommended)

```bash
git clone <your-repo>
cd omr-system
docker-compose up --build
```

Then open:
- Frontend: http://localhost:5173
- Backend API: http://localhost:5000
- OMR Engine: http://localhost:8000

### Option B: Manual Setup

**1. MongoDB** (must be running locally on `mongodb://localhost:27017`)

**2. OMR Engine (Python):**
```bash
cd omr-engine
pip install -r requirements.txt
python app.py
# Runs on http://localhost:8000
```

**3. Backend (Node):**
```bash
cd backend
cp .env.example .env   # edit if needed
npm install
npm run dev
# Runs on http://localhost:5000
```

**4. Frontend (React):**
```bash
cd frontend
npm install
npm run dev
# Runs on http://localhost:5173
```

---

## 🔑 Default Credentials

After first run, seed the DB:
```bash
cd backend && npm run seed
```

| Role     | Email                | Password    |
|----------|----------------------|-------------|
| Admin    | admin@omr.com        | admin123    |
| Evaluator| eval@omr.com         | eval123     |
| Student  | student@omr.com      | student123  |

---

## 📋 OMR Sheet Template

A printable 100-question OMR sheet is in `templates/omr_100q.html`.
Print it, fill it with a dark pen/pencil, scan it, and upload via the dashboard.

**Layout:** 100 questions, 4 options (A/B/C/D), 4 columns × 25 rows.

---

## 📡 API Documentation

See [docs/API.md](docs/API.md) for the full REST API reference.

Key endpoints:
- `POST /api/auth/login`
- `POST /api/exams` (admin)
- `POST /api/scan/upload` (multipart — answer sheet)
- `GET /api/results/:examId`
- `GET /api/analytics/:examId`

---

## 🗄️ Database Schema

See [docs/SCHEMA.md](docs/SCHEMA.md).

Collections: `users`, `exams`, `answerkeys`, `submissions`, `results`, `auditlogs`.

---

## 🛡️ Security Features

- bcrypt password hashing (10 rounds)
- JWT with 24h expiry + refresh tokens
- Role-based middleware (`requireRole('admin')`)
- QR code per OMR sheet — prevents duplicate scans
- Audit log on every state change
- Input sanitization (express-validator)
- Rate limiting on auth endpoints
- File-type whitelist on uploads
- HTTPS-ready (Nginx config included)

---

## 🧪 Testing the OMR Engine

```bash
cd omr-engine
python test_engine.py samples/test_sheet.jpg
```

Expected output: detected bubbles, per-question answers, confidence scores.

---

## 📦 Production Deployment

See [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) for AWS / DigitalOcean / VPS guides.

---

## 📜 License

MIT — free for commercial and educational use.

---

## 🙏 Acknowledgements

- OpenCV for image processing
- Tesseract OCR for roll number recognition
- jsPDF for scorecard generation
- Recharts for analytics visualizations
