# 🛡️ Reddit Fact Guard

**AI-powered real-time credibility analysis for Reddit - built in 24 hours.**

A Chrome Extension + Python backend that uses **Large Language Models (Llama 3.1 / Llama 3.2 Vision via Groq)**, **computer vision for AI-generated image detection**, **bot network heuristic analysis**, and **NLP-based community sentiment scanning** to deliver a multi-signal trust score on any Reddit post — directly in the browser.

Built during a 24-hour hackathon using [**Kiro**](https://kiro.dev) — an agentic AI IDE powered by Claude.

---

## 🧠 Tech Stack

| Layer | Technologies |
|-------|-------------|
| **AI / LLM** | Groq Cloud API, Llama 3.1 8B (text reasoning), Llama 3.2 90B Vision (image analysis) |
| **Backend** | Python, Flask, REST API, NumPy |
| **Extension** | JavaScript (ES6+), Chrome Manifest V3, DOM manipulation, Fetch API |
| **Analysis** | NLP keyword extraction, Jaccard similarity, time-series burst detection, lexical diversity scoring |
| **Data Sources** | PullPush Reddit Archive API (author history), Reddit DOM scraping (real-time) |
| **DevOps** | Git, GitHub, modular Python packaging |

---

## 🔬 Analysis Pipeline (5 Signals)

### 1. LLM Text Analysis (Groq / Llama 3.1)
Sends the full post content + comments to a large language model with a calibrated prompt. The model evaluates factual claims, source quality, emotional manipulation, and logical consistency.

### 2. AI Image Detection (Groq Vision / Llama 3.2 90B)
Downloads the post image, encodes it to base64, and sends it to a vision model that checks for AI-generation artifacts (distorted hands, inconsistent lighting, unnatural textures), manipulation, and misleading context.

### 3. Bot Network Heuristics (NumPy)
Seven independent signals computed locally with no API calls:
- **Volume dominance** - single author flooding the thread
- **Text similarity** - Jaccard coefficient between comment pairs
- **Time burst detection** - coordinated posting within 60-second windows
- **Lexical diversity** - type-token ratio indicating vocabulary poverty
- **Network topology** - reply loop detection
- **Activity hour concentration** - inhuman posting schedules
- **Text pattern analysis** - excessive caps / exclamation abuse

### 4. Community Debunking (NLP Keyword Scan)
Scans all comments against a curated lexicon of debunking terms ("deepfake", "fabricated", "misinformation", etc.) and computes a skepticism density score weighted by unique author diversity.

### 5. Author History Profiling (PullPush API)
Fetches the post author's public history from the PullPush Reddit archive to estimate account age and posting patterns — new/throwaway accounts receive a credibility penalty.

---

## 🚀 Quick Start

### Backend
```bash
cd backend
pip install -r requirements.txt

# Create .env with your Groq API key
echo GROQ_API_KEY=your_key_here > .env

python server.py
```

### Chrome Extension
1. Navigate to `chrome://extensions/`
2. Enable **Developer mode**
3. Click **Load unpacked** → select the `extension/` folder
4. Visit any Reddit post

---

## 📁 Project Structure

```
├── extension/
│   ├── manifest.json          # Chrome Manifest V3 config
│   ├── content.js             # DOM scraping + widget injection
│   └── widget.css             # Glassmorphism UI styling
├── backend/
│   ├── server.py              # Flask API + pipeline orchestration
│   ├── history_fetcher.py     # PullPush Reddit archive client
│   ├── requirements.txt
│   └── CommentAnalyzer/       # Modular analysis engine
│       ├── orchestrator.py    # Weighted score fusion
│       ├── models/
│       │   ├── comment.py     # Comment data model
│       │   └── comment_list.py
│       └── analyzers/
│           ├── bot_network_analyzer.py    # 7-signal bot detection
│           ├── community_debunking.py     # NLP keyword scanner
│           └── account_profiler.py        # Account age/karma analysis
└── README.md
```

---

## 🛠️ Development

Built in 24 hours using **Kiro** — an agentic AI IDE (similar to Claude Code) that enables rapid full-stack development through conversational programming. Kiro handled architecture decisions, code generation, debugging, and iterative refinement across the entire stack.
