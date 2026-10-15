# 🧠 Project Frankenstein: Repo 2 - The Brain (AI Backend & API)

Welcome to the **Frankenstein Web Challenge**!

> *"Did you think the brain could live without the body?"*  
> This repository contains **The Brain** — the FastAPI backend server, the weighted fuzzy matching recommendation engine (`phase1_rule_based.py`), the internship knowledge base (`internships.csv`), and ElevenLabs text-to-speech integration.
>
> However, critical pathways have been disconnected, and the security gates are locking out the frontend!
>
> **Your Goal:** Fix the severed endpoints, open the gates (CORS), and reconnect the brain to **Repo 1 (The Body)**!

---

## 📁 Repository Structure
```
repo_2_backend/
├── main.py                # ⚡ FastAPI application (CONTAINS SEVERED LOGIC & CORS BLOCK!)
├── phase1_rule_based.py   # Multi-criteria weighted fuzzy matching engine (RapidFuzz)
├── internships.csv        # Internship catalog database
├── requirements.txt       # Python package dependencies
└── .env.example           # Environment variables template
```

---

## ⚡ Your Stitching Challenges in this Repo

Look for the `⚡ [FRANKENSTEIN CHALLENGE]` markers inside `main.py`:

### 🎯 Challenge 4: The Barbed Wire (CORS Lockout)
* **File:** `main.py` (Line ~85)
* **Problem:** `CORSMiddleware` is configured to only allow `http://unauthorized-frankenstein-domain.invalid` and blocks `POST` requests and `Content-Type` headers!
* **Your Task:**
  1. Add your frontend origins (e.g. `http://localhost:3000`, `http://127.0.0.1:5500`, or `*` for testing).
  2. Allow methods: `["GET", "POST", "PUT", "DELETE", "OPTIONS"]`.
  3. Allow headers: `["*"]`.

### 🎯 Challenge 5: Lobotomized Brain (Recommendation Endpoint 501)
* **File:** `main.py` at `@app.post("/api/recommend")` (Line ~250)
* **Problem:** When the frontend sends candidate profile data, the backend throws an `HTTP 501 Not Implemented` error!
* **Your Task:**
  1. Receive the `Candidate` Pydantic model and optional query parameters (`min_score`, `remote_only`, `fresher_only`).
  2. Call `recommend(candidate.model_dump(), INTERNSHIPS, min_score=min_score, filters=filters)`.
  3. Return a `JSONResponse` with:
     ```json
     {
       "count": 10,
       "recommendations": [...],
       "candidate_profile": { ... },
       "filters_applied": { ... },
       "message": "Found 10 matching opportunities"
     }
     ```

### 🎯 Challenge 6: The Secret Juice (Environment Configuration)
* **File:** `.env.example` -> `.env`
* **Problem:** Without credentials and environment variables, TTS voice synthesis and server configuration will fail.
* **Your Task:** Copy `.env.example` to `.env` and configure your API keys.

---

## 🚀 How to Run the Backend Locally

1. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Start the FastAPI server:**
   ```bash
   uvicorn main:app --reload --port 8000
   ```

3. **Verify API Docs:**
   Open [http://localhost:8000/docs](http://localhost:8000/docs) in your browser to inspect interactive Swagger documentation!
