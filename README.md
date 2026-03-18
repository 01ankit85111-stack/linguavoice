#  LinguaVoice — Real-Time Voice Language Companion
### Built on Murf Falcon TTS API · Powered by Claude AI

---

##  Overview

**LinguaVoice** is a real-time, voice-first language learning companion that uses:
- **Murf Falcon TTS API** for natural, expressive voice responses
- **Claude AI (claude-sonnet-4-20250514)** for intelligent tutoring conversations
- **Web Speech API** for microphone-based voice input
- **Web Audio API** for real-time waveform visualization

Users can practice a new language through natural spoken conversation — the AI tutor responds in English while naturally weaving in target-language phrases, and Murf Falcon speaks the responses aloud with studio-quality voice.

---

##  Features

| Feature | Description |
|---|---|
| 🎤 Voice Input | Browser Speech Recognition for hands-free conversation |
| 🔊 Murf Falcon TTS | Studio-quality AI voice output via Murf API |
| 🧠 Claude AI Tutor | Intelligent language tutor that adapts to your level |
| 📊 Live Waveform | Real-time audio visualization during listening/speaking |
| 📝 Vocab Tracker | Automatically extracts and saves vocabulary from sessions |
| 🌍 8 Languages | Spanish, French, Japanese, German, Mandarin, Italian, Portuguese, Hindi |
| 📈 Session Stats | Track exchanges, words heard, streak, and session time |
| 🎭 Voice Selection | Multiple Murf voice personas (Natalie, Marcus, Hazel, Ken) |
| ⚡ Demo Mode | Works without API keys using browser TTS fallback |

---

## 🛠️ Setup & Usage

### 1. Open the App
Just open `index.html` in any modern browser (Chrome recommended for best Speech Recognition support).

### 2. Configure API Keys
On first launch, a setup modal appears. Enter:
- **Murf Falcon API Key** — from [murf.ai](https://murf.ai)
- **Target Language** — the language you want to learn
- **Voice** — your preferred tutor voice
- **Proficiency Level** — Beginner / Intermediate / Advanced

Or click **Demo Mode** to try with browser TTS (no API key required).

### 3. Start Talking
- **Type** in the text box and press Enter, or click ↑ Send
- **Speak** by clicking the mic button or the animated orb

---

## 🔌 Murf Falcon API Integration

```javascript
// TTS Generation Endpoint
POST https://api.murf.ai/v1/speech/generate

// Request Body
{
  "text": "¡Hola! In Spanish, we say Hola, ¿cómo estás?",
  "voiceId": "en-US-natalie",
  "format": "MP3",
  "sampleRate": 24000,
  "speed": 1.0,
  "pitch": 0,
  "style": "Conversational"
}

// Authentication
Headers: { "api-key": "YOUR_MURF_API_KEY" }

// Response
{ "audioFile": "https://...mp3" }
```

The app gracefully falls back to browser Web Speech API if Murf is unavailable.

---

## 🧠 Claude AI Tutor Prompting

The AI tutor uses a carefully designed system prompt that:
1. Responds conversationally in English with target-language words bolded
2. Extracts a `TRANSLATION:` phrase for display as a subtitle
3. Extracts `VOCAB:word=meaning` pairs for the vocabulary tracker
4. Adapts tone and complexity to the user's proficiency level

---

## 🗂️ Architecture

```
index.html (Single File App)
│
├── UI Layer (HTML/CSS)
│   ├── Conversation Panel (chat bubbles + waveform)
│   ├── Voice Orb (animated mic/speaker indicator)
│   └── Sidebar (stats, vocab, controls)
│
├── Voice Input (Web Speech API)
│   └── SpeechRecognition → text → Claude AI
│
├── AI Layer (Anthropic Claude API)
│   └── Claude Sonnet → structured response (text + translation + vocab)
│
└── Voice Output (Murf Falcon TTS)
    └── Murf API → MP3 audio URL → HTML Audio → waveform visualization
```

---

## 🎯 Use Case: Language Learning Companion

This specific implementation targets **language learners** who want to practice through natural conversation. The voice-first design means:

- No typing required — speak naturally, get spoken responses
- The orb's animated states give clear feedback (idle / listening / speaking)
- Translation subtitles appear with each AI response
- Vocabulary is automatically extracted and tracked per session
- Streak counter encourages daily practice

---

## 🔧 Extending the App

The codebase is designed to be easily extended:

```javascript
// Add a new language
// In targetLang <select>, add:
<option value="Korean">🇰🇷 Korean</option>

// Change the AI model
model: 'claude-opus-4-20250514'  // for more sophisticated tutoring

// Add new Murf voices
// Find available voiceIds in Murf dashboard and add to <select>

// Add conversation modes
// Modify system prompt for: pronunciation drill, grammar focus, roleplay scenarios
```

---

## 📦 Dependencies

| Dependency | Source | Purpose |
|---|---|---|
| Google Fonts (Syne + DM Sans) | CDN | Typography |
| Anthropic Claude API | api.anthropic.com | AI conversation |
| Murf Falcon API | api.murf.ai | Text-to-Speech |
| Web Speech API | Browser built-in | Voice input |
| Web Audio API | Browser built-in | Waveform visualization |

**Zero npm dependencies. Zero build step. Single HTML file.**

---

## 🏆 Hackathon Notes

This prototype demonstrates:
1. **Voice as Primary Interface** — mic input + spoken TTS output + visual orb feedback
2. **Real-Time AI Integration** — low-latency Claude AI responses streamed to Murf TTS
3. **Practical Use Case** — language learning with measurable session outcomes
4. **Graceful Degradation** — fallback to browser TTS if Murf API unavailable
5. **Extensibility** — easily swap languages, voices, AI models, or add new features

---


