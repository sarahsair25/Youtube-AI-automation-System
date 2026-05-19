# 🎬 YouTube AI Automation System

> Complete AI-powered YouTube content pipeline — from idea generation to video upload.

![Python](https://img.shields.io/badge/Python-3.9+-blue) ![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o-green) ![Zapier](https://img.shields.io/badge/Zapier-Automation-orange) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

---

## 🚀 What it does

No manual scripting. No thumbnail design. No copy-pasting descriptions. This pipeline handles your entire YouTube content workflow automatically — triggered weekly by Zapier and powered by GPT-4o.

| Step | Tool | Output |
|------|------|--------|
| Schedule trigger | Zapier | Weekly automation kickoff |
| Script & metadata | GPT-4o | Title, script, description, tags |
| Thumbnail | DALL-E 3 | AI-generated image with text overlay |
| Upload | YouTube Data API v3 | Published video with full metadata |
| Captions | OpenAI Whisper | Auto-generated .srt subtitles |

---

## 💸 Cost to run

| Service | Monthly Cost | Notes |
|---------|-------------|-------|
| OpenAI GPT-4o | $10–20 | 4–8 video scripts |
| DALL-E 3 | $5–10 | 4–8 thumbnails |
| Zapier | $0–20 | Free tier: 100 tasks/month |
| YouTube API | Free | 10,000 units/day quota |
| **Total** | **$15–50** | For 4–8 videos/month |

---

## 📋 Prerequisites

- Python 3.9+
- OpenAI API key
- YouTube Data API v3 credentials
- Zapier account (free tier works)
- Google Cloud project

---

## 🛠️ Installation

```bash
# 1. Clone the repo
git clone https://github.com/sarahsair25/youtube-ai-automation.git
cd youtube-ai-automation

# 2. Install dependencies
pip install -r requirements.txt

# 3. Configure environment variables
cp .env.example .env
# Edit .env with your API keys

# 4. Set up YouTube OAuth
python -c "from src.youtube_uploader import YouTubeUploader; YouTubeUploader()"
# Follow the OAuth flow in your browser
```

---

## 📖 Usage

### Quick start

```python
from src.content_generator import YouTubeContentGenerator
from src.thumbnail_generator import ThumbnailGenerator

generator = YouTubeContentGenerator()
video = generator.generate_video_plan("How to use LangChain for RAG")
generator.save_script(video)

thumb_gen = ThumbnailGenerator()
thumb_gen.generate_thumbnail(video.thumbnail_prompt, video.title)
```

### Full weekly pipeline

```bash
python main.py          # Run with scheduling
python main.py --test   # Test run, no scheduling
```

### Optional: Custom voiceover with ElevenLabs

```python
from elevenlabs import generate, save

audio = generate(text=video.script, voice="Adam", model="eleven_monolingual_v1")
save(audio, "voiceover.mp3")
```

---

## ⚡ Zapier Configuration

| Step | App | Action |
|------|-----|--------|
| 1 | Schedule by Zapier | Trigger every Monday 9:00 AM |
| 2 | AI by Zapier (GPT-4o) | Generate script & metadata |
| 3 | Google Docs | Save generated script |
| 4 | Webhook | Send data to Python backend |

---

## 🔧 Troubleshooting

| Issue | Fix |
|-------|-----|
| YouTube upload fails | Check OAuth token expiry |
| GPT-4o rate limits | Add exponential backoff |
| Thumbnail errors | Verify DALL-E prompt length |
| Zapier webhook timeout | Switch to polling |

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

---

## 📄 License

MIT — free to use, remix, and build on.

---

## 🙏 Acknowledgments

- [OpenAI](https://openai.com) for GPT-4o and DALL-E 3
- [Zapier](https://zapier.com) for workflow automation
- [Google](https://developers.google.com/youtube) for the YouTube Data API
