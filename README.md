# AUTONOMOUS-SOCIAL-MEDIA-BRAND-MANAGER-USING-MULTI-AGENTS-FOR-TEXT-GENERATING-ASMB-
Multi-Agent AI System (CrewAI + OpenAI)

---

## Architecture

```
social_media_manager/
├── config/
│   └── settings.py          # Module 1 — all config, paths, env vars
├── data/
│   ├── brand_guidelines/    # Module 2 — brand docs (edit sample_brand.txt)
│   └── mock_metrics/        # Module 2 — simulated engagement data
├── tools/                   # Module 3 — 4 custom tools
│   ├── brand_knowledge_tool.py
│   ├── sentiment_tool.py
│   ├── mock_social_api.py
│   └── platform_formatter.py
├── agents/                  # Module 4 — 5 specialised agents
│   ├── strategy_agent.py
│   ├── content_agent.py
│   ├── brand_voice_agent.py
│   ├── engagement_agent.py
│   └── analysis_agent.py
├── tasks/                   # Module 5 — task definitions
│   └── task_definitions.py
├── crew/                    # Module 6 — crew orchestrator
│   └── social_media_crew.py
├── main.py                  # Module 7 — CLI entry point
├── app.py                   # Module 8 — Streamlit web UI
├── outputs/                 # Auto-created — JSON campaign results
├── requirements.txt
└── .env.example
```

---

## Setup

```bash
# 1. Clone / copy project
cd social_media_manager

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Set your API key
cp .env.example .env
# Edit .env and add your OPENAI_API_KEY=sk-...
```

---

## Running the project

### Option A — Streamlit UI (recommended)
```bash
streamlit run app.py
```
Open http://localhost:8501 in your browser.

### Option B — CLI
```bash
python main.py \
  --brief "Launch our new Eclipse Espresso blend for autumn" \
  --platforms Instagram LinkedIn
```

---

## Agents

| Agent | Role | Key Tools |
|---|---|---|
| Strategy Agent | Plans campaign, sets KPIs | Brand guidelines, metrics |
| Content Agent | Writes posts and captions | Brand knowledge, formatter |
| Brand Voice Agent | Reviews tone, approves/revises | Brand guidelines, formatter |
| Engagement Agent | Replies to comments | Sentiment analysis, comments |
| Analysis Agent | Reads metrics, produces insights | Metrics, sentiment |

---

## Tools

| Tool | Purpose |
|---|---|
| `BrandKnowledgeTool` | Keyword search over brand guidelines |
| `BrandGuidelinesLoaderTool` | Loads full guidelines document |
| `SentimentAnalysisTool` | VADER-based comment sentiment classification |
| `MockPostTool` | Simulates posting (logs to outputs/) |
| `MockFetchCommentsTool` | Returns sample comments from mock data |
| `MockFetchMetricsTool` | Returns 30-day simulated metrics |
| `PlatformFormatterTool` | Validates character limits + hashtag counts |

---

## Customising for a real brand

1. Replace `data/brand_guidelines/sample_brand.txt` with your brand document.
2. Replace `data/mock_metrics/sample_metrics.json` with real or updated metrics.
3. For real posting: replace `MockPostTool` with real API wrappers
   (Instagram Graph API, Twitter API v2, LinkedIn API).
4. For web trend search: add `SerperDevTool` from crewai-tools and assign it
   to the Strategy Agent. Set `SERPER_API_KEY` in `.env`.

---

## Evaluation (FYP)

To demonstrate the multi-agent advantage:
1. Run the system for a fictional brand (sample_brand.txt is ready).
2. Run the same brief through a single GPT-4 prompt (no agents).
3. Have human evaluators rate: brand consistency, engagement quality, completeness.
4. Compare scores.

Expected result: multi-agent system scores higher on consistency and completeness.

---

## Future extensions

- Swap `gpt-4o-mini` for local Ollama model (set `LLM_MODEL=ollama/llama3`)
- Add FAISS vector store for multi-document brand knowledge
- Add scheduling simulation with APScheduler
- Replace mock APIs with real platform integrations
- Add A/B variant generation (content agent produces 2 versions, brand agent picks one)
