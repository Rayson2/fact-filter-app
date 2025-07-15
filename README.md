
# 🧠 Fact Filter — Fullstack Monorepo (Frontend + Backend)

**Fact Filter** is a full-stack AI-powered misinformation detection system that supports multiple content formats: text, image, audio, and video. It uses state-of-the-art technologies including **OpenAI Whisper**, **Gemini Pro**, and a custom **NLP model** to classify information as **Fake**, **Real**, or **Opinion**.  

This monorepo contains:
- 🧩 **Frontend**: A React + SCSS UI
- 🔧 **Backend**: FastAPI service with Whisper, Gemini, and NLP integrations

---


## 📁 Repository Structure

```

fact-filter/
├── frontend/        # React app (Vite + SCSS)
│   ├── src/
│   └── .env         # API base URL and EmailJS keys
│
├── backend/         # FastAPI server
│   ├── app/
│   ├── requirements.txt
│   └── .env         # Gemini API key
│
├── README.md        # Monorepo documentation
└── LICENSE

````

---

## 🚀 Features

### 🌐 Frontend
- 🎥 Upload video/audio/image/text for fact-checking
- 🧠 Choose between **Gemini API** and **Custom NLP**
- 💬 Get detailed results: **Real**, **Fake**, or **Opinion**
- 💅 Responsive and modern UI using SCSS
- 📤 EmailJS integration (for future features)

### 🖥️ Backend
- 🗣️ **Whisper**: Transcribes audio/video using `faster-whisper`
- 📸 **Tesseract OCR**: Extracts text from images
- 🧠 **Custom NLP model**: Logistic Regression + TF-IDF
- 💡 **Gemini Pro**: Google’s large language model for advanced fact-checking
- 📈 CSV logging of all results
- 🔒 Rate limiting to prevent abuse

---

## 🔧 Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/rayson2/fact-filter-app.git
cd fact-filter-app
````

---

## 📦 Backend Setup (`backend/`)

### Prerequisites

* Python 3.10+
* ffmpeg (must be in system PATH) → [Download FFmpeg](https://ffmpeg.org/download.html)
* Tesseract OCR → [Download Tesseract](https://github.com/tesseract-ocr/tesseract)

### Installation

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

### .env Configuration

Create `backend/app/.env` with:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

### Download & Train NLP Model

1. Download from: [Fake News Dataset – Kaggle](https://www.kaggle.com/datasets/emineyetm/fake-news-detection-datasets)
2. Place `Fake.csv` and `True.csv` in:

```
backend/app/nlp_util/data/
```

3. Train:

```bash
python app/nlp_util/train_model.py
```

### Run the FastAPI server

```bash
uvicorn app.main:app --reload
```

---

## 💻 Frontend Setup (`frontend/`)

### Prerequisites

* Node.js ≥ 18
* npm

### Installation

```bash
cd frontend
npm install
```

### .env Configuration

Create `frontend/.env` with:

```env
VITE_API_BASE_URL=http://0.0.0.0:8000
REACT_APP_EMAILJS_SERVICE_ID=service
REACT_APP_EMAILJS_TEMPLATE_ID=template
REACT_APP_EMAILJS_PUBLIC_KEY=your_public_key
```

### Start the development server

```bash
npm run dev
```

---

## 📡 API Endpoints

| Method | Endpoint                | Description                        |
| ------ | ----------------------- | ---------------------------------- |
| POST   | `/fact-check-text`      | Check raw text                     |
| POST   | `/fact-check-image`     | OCR + fact-check on image text     |
| POST   | `/fact-check-audio`     | Transcribe + check audio           |
| POST   | `/fact-check-video`     | Transcribe + check video           |
| GET    | `/fact-check-results` | Get logged results (NLP or Gemini) |
| GET    | `/`                     | Check API status                   |

> Set `source=nlp` or `source=gemini` in request query or form.

---

## 🔐 Rate Limiting

Each client IP is limited to **5 requests per 60 seconds**.
Returns `429 Too Many Requests` if exceeded.

---

## 🎨 UI & Styling

* Built with **React + SCSS**
* Clean, responsive layout
* Theming using SCSS variables:

  ```scss
  $primary-color: #53a1d6;
  $secondary-color: #f0f0f0;
  $text-color: #1a1a1a;
  ```

---

## 📤 Deployment

You can deploy:

* Frontend via **Vercel** or **Netlify**
* Backend via **Render**, **Railway**, or **your own server**


---

## 👨‍💻 Developer

* **Rayson** — Fullstack development, AI integration, UI/UX

---

## 📝 License

This project is licensed under the **MIT License**.
See the [LICENSE](./LICENSE) file for full terms.

---

## 🧠 Acknowledgements

* [OpenAI Whisper](https://github.com/openai/whisper)
* [Google Gemini Pro](https://deepmind.google/technologies/gemini/)
* [Tesseract OCR](https://github.com/tesseract-ocr/tesseract)
* [Fake News Dataset](https://www.kaggle.com/datasets/emineyetm/fake-news-detection-datasets)


