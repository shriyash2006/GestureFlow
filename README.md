<div align="center">

# 🎄 GestureFlow
### Autonomous Holiday Design Studio & Gesture-Controlled 3D Experience
#### Powered by Google Agent Development Kit (ADK), Model Context Protocol (FastMCP), and Vertex AI Memory Bank

[![Python Version](https://img.shields.io/badge/Python-3.11%20%7C%203.12-3776AB?logo=python&logoColor=white)](https://python.org)
[![Google ADK](https://img.shields.io/badge/Google-ADK-4285F4?logo=google&logoColor=white)](https://github.com/google/adk)
[![Model Context Protocol](https://img.shields.io/badge/MCP-FastMCP-8A2BE2?logo=databricks&logoColor=white)](https://github.com/modelcontextprotocol)
[![Gemini & Imagen](https://img.shields.io/badge/Models-Gemini%202.5%20Flash%20%7C%20Imagen-FF6F00?logo=google-gemini&logoColor=white)](https://ai.google.dev)
[![React & Three.js](https://img.shields.io/badge/Frontend-React%20%7C%20Three.js%20%7C%20Vite-61DAFB?logo=react&logoColor=black)](https://threejs.org)
[![MediaPipe](https://img.shields.io/badge/Vision-MediaPipe%20HandLandmarker-0097A7?logo=google&logoColor=white)](https://developers.google.com/mediapipe)
[![FastAPI](https://img.shields.io/badge/Backend-FastAPI-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com)
[![License](https://img.shields.io/badge/License-Apache%202.0-2E7D32.svg)](LICENSE)

<br/>

**GestureFlow** is a next-generation generative AI studio and interactive holiday centerpiece. It merges **Google Agent Development Kit (ADK)** cognitive orchestration, **FastMCP** image generation tool pipelines, **MediaPipe** webcam hand gesture recognition, and an interactive **Three.js** 3D Christmas tree with persistent long-term memory recall.

[Architecture](#-system-architecture) • [Key Features](#-key-features) • [Generative Tools](#-mcp-generative-pipeline) • [Gesture Controls](#-interactive-hand-gestures) • [Project Structure](#-project-structure) • [Quickstart](#-getting-started) • [Memory Bank](#-session-continuity--memory-bank)

---

</div>

## 📌 Overview

Based on Google's Developer Codelab: **"Building Personalized Agents with ADK, MCP, and Memory Bank"**, **GestureFlow** transforms raw multimodal inputs into custom holiday cards and interactive 3D holiday environments. 

The system operates across three core pillars:
1. **Tooling Layer (Model Context Protocol - FastMCP):** Exposes Python generative functions via FastMCP standard protocols to Gemini models.
2. **Cognitive Orchestration Layer (Google ADK):** An autonomous planning agent (`christmas_agent`) that interprets free-form creative prompts, decomposes goals into dependent multi-step workflows, and controls 3D tree states.
3. **Context & State Layer (ADK Session & Vertex AI Memory Bank):** Maintains short-term dialog state and long-term user style preferences (aesthetic, themes, motifs) across distinct sessions and server restarts.

---

## 🏛️ System Architecture

```text
 ┌──────────────────────────────────────────────────────────────────────────┐
 │                           USER INTERACTION LAYER                         │
 │                                                                          │
 │   ┌───────────────────────────────┐     ┌────────────────────────────┐   │
 │   │      Interactive 3D Tree      │     │    Webcam Gesture Sense    │   │
 │   │  (Three.js / React Fiber)     │     │  (MediaPipe HandLandmarker)│   │
 │   └───────────────┬───────────────┘     └─────────────┬──────────────┘   │
 │                   │                                   │                  │
 │                   │     ┌───────────────────────┐     │                  │
 │                   └────>│  Chat & Upload Modal  │<────┘                  │
 │                         └───────────┬───────────┘                        │
 └─────────────────────────────────────┼────────────────────────────────────┘
                                       │ HTTP / WebSocket (Port 8001)
                                       ▼
 ┌──────────────────────────────────────────────────────────────────────────┐
 │                        APPLICATION BACKEND (FastAPI)                     │
 │                                                                          │
 │     ┌──────────────────────────────────────────────────────────────┐     │
 │     │                Google ADK Runner Orchestration               │     │
 │     └──────────────┬───────────────────────────────┬───────────────┘     │
 │                    │                               │                     │
 │                    ▼                               ▼                     │
 │       ┌────────────────────────┐      ┌─────────────────────────┐        │
 │       │     Session Service    │      │       Memory Bank       │        │
 │       │ (InMemory / Vertex AI) │      │ (InMemory / Vertex AI)  │        │
 │       └────────────────────────┘      └─────────────────────────┘        │
 │                    │                                                     │
 │                    ▼                                                     │
 │       ┌────────────────────────┐                                         │
 │       │    Christmas Agent     │◄─── Models: Gemini 2.5 Flash            │
 │       │   (Cognitive Engine)   │             Imagen 3                    │
 │       └────────────┬───────────┘                                         │
 └────────────────────┼─────────────────────────────────────────────────────┘
                      │
                      │ Standard I/O (Model Context Protocol)
                      ▼
 ┌──────────────────────────────────────────────────────────────────────────┐
 │                          FastMCP TOOL SERVER                             │
 │                                                                          │
 │  ┌───────────────────────┐ ┌───────────────────────┐ ┌────────────────┐ │
 │  │ generate_holiday_scene│ │generate_sweater_pattern│ │generate_wearing│ │
 │  └───────────────────────┘ └───────────────────────┘ └────────────────┘ │
 │                             ┌─────────────────────┐                      │
 │                             │generate_final_photo │                      │
 │                             └─────────────────────┘                      │
 └──────────────────────────────────────────────────────────────────────────┘
```

### Architectural Visualizations

The repository includes detailed architectural schematics for every layer:

| Component Architecture | Memory Bank Lifecycle |
| :---: | :---: |
| <img src="03-Connect-ADK-MCP-UI/02-solution/architecture_diagram.svg" width="460" alt="Architecture Diagram"/> | <img src="03-Connect-ADK-MCP-UI/02-solution/memory_bank_diagram.svg" width="460" alt="Memory Bank Diagram"/> |

| Agent-MCP Protocol Flow | Memory Comparison (Short vs. Long Term) |
| :---: | :---: |
| <img src="03-Connect-ADK-MCP-UI/02-solution/agent_mcp_connection.svg" width="460" alt="Agent MCP Connection"/> | <img src="03-Connect-ADK-MCP-UI/02-solution/memory_comparison.svg" width="460" alt="Memory Comparison"/> |

---

## ✨ Key Features

* **Real-Time Hand Gesture Navigation:** Track 21 hand 3D landmarks at 60 FPS using MediaPipe WebGL delegate; manipulate camera angles, collapse tree structures, or trigger particle explosions hands-free.
* **Autonomous Multi-Step Generation:** Decomposes complex user requests (*"Make a holiday scene with my puppy in a snowy mountain sweater"*) into coordinated tool sequences.
* **Texture & Knit Pattern Synthesis:** Generates 1:1 seamless, tileable 2D knit texture patterns using custom prompt modifiers.
* **Multimodal Facial Feature Adaptation:** Analyzes uploaded subject photos and synthesizes personalized avatars wearing the generated sweater pattern.
* **Cinematic 50mm Composite Rendering:** Composites the avatar, custom sweater, and holiday landscape into a warm, framed fireplace mantelpiece photo.
* **Dynamic 3D Christmas Tree:** Renders procedural pine needles, custom star toppers, glowing fairy lights, and dynamic polaroid picture galleries.
* **Dual-Tier Memory Continuity:** Retains conversational context during active sessions and stores long-term style preferences across restarts using Vertex AI Memory Bank.

---

## 🛠️ MCP Generative Pipeline

The FastMCP server exposes four generative endpoints directly to the ADK Agent:

| Tool Name | Parameters | Output | Description |
| :--- | :--- | :--- | :--- |
| `generate_holiday_scene` | `interest: str` | `16:9 PNG` | Creates a cinematic 3D winter landscape incorporating the user's specific theme or interests. |
| `generate_sweater_pattern` | `motif: str` | `1:1 PNG` | Generates a seamless, tileable 2D knit ugly-sweater pattern texture map. |
| `generate_wearing_sweater` | `image_path: str`<br/>`pattern_description: str` | `1:1 PNG` | Extracts character traits from an uploaded photo and renders a cute avatar dressed in the custom pattern. |
| `generate_final_photo` | *None* | `16:9 PNG` | Composites the sweater avatar and holiday scene into a framed mantelpiece photo with warm bokeh. |

### Auxiliary Tree State Tools
* `update_tree_config(config_key, value)`: Updates 3D tree properties (`lights_color`, `ornament_texture`, `theme`).
* `get_tree_state()`: Queries current tree parameters.
* `analyze_image_and_suggest_texture(image_description)`: Vision-based theme extraction.

### Sample Generated Assets

<div align="center">

| Personalized Avatar | Custom Knit Pattern | Holiday Scene |
| :---: | :---: | :---: |
| <img src="03-Connect-ADK-MCP-UI/02-solution/backend/static/generated_selfie.png" width="220" alt="Generated Selfie"/> | <img src="03-Connect-ADK-MCP-UI/02-solution/backend/static/generated_pattern.png" width="220" alt="Generated Pattern"/> | <img src="03-Connect-ADK-MCP-UI/01-starter/frontend/src/photos/cute_cat_christmas.png" width="220" alt="Cute Cat Holiday"/> |

</div>

---

## 🖐️ Interactive Hand Gestures

GestureFlow features a browser-based computer vision engine that tracks hand poses via webcam:

| Gesture | Action | 3D Tree Behavior |
| :--- | :--- | :--- |
| 🖐️ **Open Palm (≥ 4 fingers)** | **Unleash / Chaos Mode** | Tree dissolves into a floating particle storm; polaroid cards float freely in 3D orbit. |
| ✊ **Fist / Closed Hand** | **Formed Tree Mode** | Ornaments, lights, and polaroids assemble neatly onto the pine branches. |
| ✋ **Hand Movement (X/Y)** | **Orbital Camera Pan** | Tracks palm center position to rotate and tilt the 3D scene smoothly in real-time. |

> [!NOTE]
> All gesture processing executes locally on the client via WebAssembly and WebGL shaders without transmitting video feeds to any remote server.

---

## 📂 Project Structure

The project is structured into four sequential workshop stages:

```bash
GestureFlow/
├── 01-MCP-Files-Testing/              # Stage 1: MCP Tool Declaration & Pipeline Testing
│   ├── 01-starter/                    # FastMCP tool skeleton
│   │   ├── mcp_server.py
│   │   └── pyproject.toml
│   └── 02-solution/                   # Completed tool implementations & image generation
│       ├── mcp_server.py
│       └── pyproject.toml
├── 02-Vibe-Coding-ADK-Agent/          # Stage 2: ADK Agent Creation & Vibe Coding
│   ├── 01-starter/                    # Starter agent configuration
│   └── 02-solution/                   # Completed ADK agent connected to local FastMCP
│       ├── mcp_server.py
│       ├── pyproject.toml
│       └── root_agent/
│           ├── __init__.py
│           └── agent.py
├── 03-Connect-ADK-MCP-UI/              # Stage 3: Full-Stack Web App & 3D Visualizer
│   ├── 01-starter/                    # Skeleton backend & frontend
│   └── 02-solution/                   # Production-ready integration
│       ├── backend/                   # FastAPI service with ADK Runner
│       │   ├── agent.py
│       │   ├── main.py
│       │   └── mcp_server.py
│       ├── frontend/                  # React + Three.js + MediaPipe UI
│       │   ├── components/            # TreeStar, Ornaments, Polaroids, GestureController
│       │   ├── public/models/         # hand_landmarker.task MediaPipe asset
│       │   └── App.tsx
│       └── start_app.sh               # Single-command fullstack launcher
├── 04-Adding-Memory-Bank/             # Stage 4: Persistent Personalization
│   ├── 01-starter/                    # Starter with InMemory sessions
│   └── 02-solution/                   # Vertex AI Memory Bank & Session Service integration
│       ├── backend/
│       │   ├── agent.py
│       │   ├── deploy_agent.py        # Agent Engine provisioning script
│       │   └── main.py
│       ├── start_app.sh
│       └── use_memory_bank.sh         # Memory Bank activation toggle
├── billing-enablement.py              # Cloud project setup helper
├── init.sh                            # Workshop environment initializer
└── set_env.sh                         # GCP environment variable loader
```

---

## 🚀 Getting Started

### Prerequisites

* **Python 3.11+**
* **Node.js 18+** & npm
* **[uv](https://github.com/astral-sh/uv)** (fast Python package manager)
* A **Google AI Studio API Key** (`GEMINI_API_KEY`) or an authenticated **Google Cloud Project** (`gcloud auth login`)

---

### Step 1: Clone and Configure Environment

```bash
git clone https://github.com/shriyash2006/GestureFlow.git
cd GestureFlow
```

Create a root `.env` file or export your credentials:

```bash
# Option A: Using Google AI Studio API Key (Local Development)
export GOOGLE_API_KEY="your-gemini-api-key"
export GOOGLE_GENAI_USE_VERTEXAI="False"

# Option B: Using Google Cloud Vertex AI
export PROJECT_ID="your-google-cloud-project-id"
export LOCATION="us-central1"
export GOOGLE_GENAI_USE_VERTEXAI="True"
```

---

### Step 2: Test MCP Tool Server (Standalone)

Verify that FastMCP and the image generation pipelines are functional:

```bash
cd 01-MCP-Files-Testing/02-solution
uv run python mcp_server.py
```

The FastMCP server will start over standard I/O and verify Gemini connectivity.

---

### Step 3: Interactive Vibe-Coding with ADK Web UI

Test the cognitive planning agent directly inside the ADK Web Inspector:

```bash
cd 02-Vibe-Coding-ADK-Agent/02-solution
uv run adk web --port 8000
```

Open `http://localhost:8000` in your browser to chat with the agent and inspect tool-call arguments in real time.

---

### Step 4: Launch Full-Stack Application (Frontend + Backend)

To launch the complete interactive experience with the 3D Christmas Tree, gesture controls, and generative chat:

```bash
cd 03-Connect-ADK-MCP-UI/02-solution
chmod +x start_app.sh
./start_app.sh
```

This script:
1. Starts the **FastAPI backend** on `http://localhost:8001`
2. Installs frontend dependencies and launches the **Vite dev server** on `http://localhost:3010`

Open your browser to **`http://localhost:3010`**, enable webcam access for gestures, and start designing!

---

### Step 5: Enable Vertex AI Memory Bank (Stage 4)

To persist preferences across restarts using Vertex AI Agent Engine:

```bash
cd 04-Adding-Memory-Bank/02-solution

# 1. Provision the Vertex AI Agent Engine resource
uv run deploy_agent.py

# 2. Export the returned Agent Engine ID
export AGENT_ENGINE_ID="projects/.../locations/us-central1/reasoningEngines/..."
export USE_MEMORY_BANK="true"

# 3. Launch with Memory Bank enabled
./start_app.sh
```

---

## 🧠 Session Continuity & Memory Bank

GestureFlow employs a two-tier memory architecture to differentiate between ephemeral context and permanent style preferences:

```text
┌────────────────────────────────────────────────────────────────────────┐
│                        MEMORY LIFECYCLE MANAGEMENT                     │
│                                                                        │
│   User: "I love vintage 80s sci-fi aesthetic and neon teal accents"    │
│                                │                                       │
│                                ▼                                       │
│   ┌──────────────────────────────────────────────────────────────┐     │
│   │               ADK Runner Context Analysis                    │     │
│   └───────────────┬──────────────────────────────┬───────────────┘     │
│                   │                              │                     │
│                   ▼                              ▼                     │
│    ┌─────────────────────────────┐┌──────────────────────────────┐    │
│    │     Session Service         ││         Memory Bank          │    │
│    │ (Short-Term Conversational) ││ (Long-Term User Preferences) │    │
│    ├─────────────────────────────┤├──────────────────────────────┤    │
│    │ • Active uploaded file paths││ • Preferred style: "80s neon"│    │
│    │ • Pending tool invocations  ││ • Color palette: "Teal/Gold" │    │
│    │ • Current conversation turn ││ • Subject: "Golden Retriever"│    │
│    │                             ││                              │    │
│    │ [Cleared when session ends] ││ [Persistent across sessions] │    │
│    └─────────────────────────────┘└──────────────────────────────┘    │
└────────────────────────────────────────────────────────────────────────┘
```

| Dimension | Short-Term Session (`VertexAiSessionService`) | Long-Term Memory (`VertexAiMemoryBankService`) |
| :--- | :--- | :--- |
| **Storage Scope** | Current active chat dialog | Global per-user profile across all sessions |
| **Stored Content** | Uploaded image paths, pending tool calls, turn order | Aesthetic preferences, favorite themes, recurring motifs |
| **Lifecycle** | Ephemeral; reset upon tab close or new session | Persistent in Google Cloud Vertex AI Agent Engine |
| **Fallback** | `InMemorySessionService` | `InMemoryMemoryService` |

---

## 💬 Sample Agent Dialogue

Here is an example of the ADK Agent planning and executing a multi-tool design workflow:

```text
User: "Hi! Can you create a personalized holiday card for me? Here is a photo of my dog."
[Uploaded: IMG_6147.jpeg]

Agent: "I'd love to help! What kind of holiday scene or theme do you envision?"

User: "Let's do a cozy alpine winter cabin with an ugly sweater full of starry constellations."

Agent Planning & Execution:
  ├── [Tool Call] generate_sweater_pattern(motif="starry constellation knit pattern with golden stars")
  │     └── Output: static/generated_pattern.png
  ├── [Tool Call] generate_wearing_sweater(image_path="/abs/path/to/IMG_6147.jpeg", pattern_description="starry constellations")
  │     └── Output: static/generated_selfie.png
  ├── [Tool Call] generate_holiday_scene(interest="cozy alpine winter cabin with snow covered pine trees")
  │     └── Output: static/generated_scene.png
  ├── [Tool Call] generate_final_photo()
  │     └── Output: static/final_photo.png
  └── [Tool Call] update_tree_config(config_key="lights_color", value="golden_warm")

Agent: "Your personalized holiday card is ready! 🌟 I've dressed your dog in a custom constellation knit sweater, nestled inside a warm alpine cabin scene, and placed it on the mantelpiece beside the fireplace. I've also tuned the tree lights to match the golden starlight!"
```

---

## 🔧 Troubleshooting & Tips

* **MediaPipe Model Loading Issues:** If hand tracking fails to initialize, ensure the model file is downloaded into `frontend/public/models/`:
  ```bash
  cd 03-Connect-ADK-MCP-UI/02-solution/frontend
  npm run download-model
  ```
* **Vertex AI vs. API Key Conflict:** Vertex AI SDK requires that `GOOGLE_API_KEY` is not present when using `PROJECT_ID`. The FastAPI backend (`main.py`) handles this cleanup automatically upon initialization.
* **Port Availability:**
  * Backend runs on **8001** (or 8000 for `adk web`).
  * Frontend Vite server runs on **3010** (falls back to 3011+ if occupied).
* **Permissions in Cloud Shell:** Ensure executable permissions on helper scripts:
  ```bash
  chmod +x init.sh set_env.sh start_app.sh use_memory_bank.sh
  ```

---

## 📜 License

Distributed under the **Apache 2.0 License**. See [`LICENSE`](LICENSE) for full details.

## 🤝 Acknowledgements

* **Google Developer Codelab**: *"Building Personalized Agents with ADK, MCP, and Memory Bank"*
* **Agent Development Kit (ADK)**: [Google Cloud Platform](https://github.com/google/adk)
* **Model Context Protocol (MCP)**: [FastMCP Python SDK](https://github.com/modelcontextprotocol)
* **Frontend 3D Visualizer**: Adapted from [blackboxo/christmas-tree](https://github.com/blackboxo/christmas-tree) with MediaPipe vision integration.
