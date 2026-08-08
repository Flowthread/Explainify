<div align="center"> 
<img width="160" height="160" alt="Explainify Logo" src="./public/logo.png" /> 

# Explainify 
</div> 

**Explainify** – Type any topic, get a narrated educational animation in minutes. Built for neurodivergent learners who absorb information better through visuals and audio. 

<div align="center"> 

## Demo 
![Explainify in action](./public/output6.mp4) 

</div> 

--- 

## 🎬 Generated Video Example 

A real video Explainify produced for the topic *"How do machines learn to recognize MNIST dataset numbers?"* — storyboard → Manim animation → narration → final MP4.

<div align="center">
  <img src="./public/output3.gif" alt="Generated Video Example" width="600" />
</div>


---

## 🧠 The Problem

Most educational content is text‑heavy and static.  
For neurodivergent learners (ADHD, dyslexia, autism), this creates friction:

- Too much text → cognitive overload  
- Abstract concepts → hard to visualize  
- One‑size‑fits‑all explanations → don't always click  

**Explainify changes that.**

---

## ✨ How It Works

1. **Type any topic** – e.g., *"How does a solar cell work?"*  
2. **AI generates a storyboard** – breaks the topic into scenes with narration.  
3. **Manim animations** – each scene becomes a professional animated visual.  
4. **Natural voiceover** – synced with the animation (audio duration is passed back into the animation prompt so visuals match the narration).  
5. **Comprehension check** *(roadmap)* – after watching, the AI asks one micro‑question to verify understanding.  
6. **Re‑frame loop** *(roadmap)* – on a wrong answer, Explainify picks a new representation strategy (causal diagram, concrete analogy, step‑by‑step) and regenerates the video.

This adaptive loop is **our unique differentiator** – it discovers *how* the learner understands and changes the representation until it clicks.

---

## 🔥 Key Features

| Feature | Description |
|---------|-------------|
| **Multi‑LLM support** | Auto fallback between Claude and OpenAI. |
| **Auto‑storyboard** | AI generates a scene‑by‑scene script with timings. |
| **TTS narration** | Natural voiceover with audio‑duration‑synced animations. |
| **Manim animations** | Professional mathematical and scientific visualizations. |
| **Code repair loop** | Generated Manim code is auto‑fixed on render errors (up to 3 retries). |
| **Comprehension check** *(roadmap)* | One micro‑question after each video – tests real understanding. |
| **Re‑frame loop** *(roadmap)* | On wrong answer, AI picks a new representation strategy and re‑renders. |
| **Neurodivergent‑friendly** | Low cognitive load, visual‑first, audio‑optional. |

---

## 🏗️ Architecture

Explainify is a multi‑agent pipeline that orchestrates several specialized components:

```mermaid
graph TB
    subgraph Input
        A[User Topic]
    end
    
    subgraph "LLM Configuration"
        B[setup_llm_client]
        B1[Claude API]
        B2[OpenAI API]
        B -->|Priority 1| B1
        B -->|Fallback| B2
    end
    
    subgraph "Agent 1: Script Generation"
        C[animations.py]
        C1[generate_script_json]
        C --> C1
    end
    
    subgraph "Agent 2: TTS Generation"
        D[tts_generator.py]
        D1[generate_complete_audio]
        D2[generate_audio_fragment]
        D3[concatenate_audio_fragments]
        D1 --> D2
        D2 --> D3
    end
    
    subgraph "Agent 3: Manim Code Generation"
        E[manim_generator.py]
        E1[generate_manim_code]
        E --> E1
    end
    
    subgraph "Agent 4: Video Compilation"
        F[concat_video.py]
        F1[compile_video]
        F2[concatenate_videos]
        F3[merge_video_and_audio]
        F1 --> F2
        F2 --> F3
    end
    
    subgraph Output
        G[Final Video with Audio]
    end
    
    A --> B
    B --> C1
    C1 -->|video-output.json| D1
    C1 -->|video-output.json| E1
    D1 -->|audio durations| E1
    E1 -->|.py files| F1
    F1 -->|.mp4 fragments| F2
    D3 -->|audio.mp3| F3
    F2 -->|output_silent.mp4| F3
    F3 --> G
    
    style A fill:#e1f5ff
    style G fill:#c8e6c9
    style C fill:#fff9c4
    style D fill:#ffe0b2
    style E fill:#f8bbd0
    style F fill:#d1c4e9
```

---

## 📦 Installation

### Prerequisites

- Python 3.11+
- `uv` (fast Python package manager)
- Manim, FFmpeg, LaTeX (all included in Docker)

### Quick start (using Docker – recommended)

```bash
git clone https://github.com/Flowthread/Explainify.git
cd Explainify
docker compose up
```

Then open `http://localhost:5000`.

### Local setup (without Docker)

```bash
# Install uv
curl -LsSf https://astral.sh/uv/install.sh | sh

# Clone and setup
git clone https://github.com/Flowthread/Explainify.git
cd Explainify
uv sync
source .venv/bin/activate   # or .venv\Scripts\activate on Windows
cp .env.example .env

# Start Flask server
python src/main.py
```

Then open your browser and navigate to `http://localhost:5000`.

---

## 🔑 API Keys

Explainify supports **Claude** and **OpenAI** as LLM providers. Configure at least one in `.env`:

```
CLAUDE_API_KEY=your_key        # priority 1 (used in auto mode)
OPENAI_API_KEY=your_key        # fallback; also required for TTS
```

Auto mode uses Claude first, then falls back to OpenAI. You can also force a provider in the UI.

---

## 🎯 Demo Video

Watch a 3‑minute walkthrough (link to be added):  
`https://youtu.be/your-link-here`

---

## 📁 Repository Structure

```
Explainify/
├── src/
│   ├── animations.py          # Storyboard generation
│   ├── manim_generator.py     # Manim code + repair loop
│   ├── tts_generator.py       # TTS narration
│   ├── concat_video.py        # Video + audio merging
│   ├── video_generator.py     # Job orchestration
│   └── main.py                # Flask API server
├── public/                    # Demo GIFs, logos
├── .env.example
├── Dockerfile
├── docker-compose.yml
├── README.md
└── LICENSE (MIT)
```

---

## 📄 License

**MIT License** – free to use, modify, and distribute.

---

## 🙌 Built for IncludAI 2026

Explainify was created for the [IncludAI – Neurodiversity Hackathon](https://includai-2026.devpost.com) as a tool that makes learning accessible through visual and auditory content.

---

## 📬 Contact

- GitHub: [github.com/Flowthread/Explainify](https://github.com/Flowthread/Explainify)
- Issues: [github.com/Flowthread/Explainify/issues](https://github.com/Flowthread/Explainify/issues)
- Developer: [@Flowthread](https://github.com/Flowthread)


