# LLM Cost & Token Efficiency Analyzer

A data-driven benchmarking notebook that compares **14 LLMs across 5 providers** on cost, latency, token usage, and accuracy — with support for both free-tier and paid-tier API keys.

---

## Providers Covered

| Tier | Provider | Models |
|------|----------|--------|
| Free | **Groq** | llama-3.1-8b-instant, llama-3.3-70b-versatile, mixtral-8x7b-32768, gemma2-9b-it |
| Free | **Google Gemini** | gemini-1.5-flash, gemini-2.0-flash-exp |
| Free | **Cerebras** | llama3.1-8b, llama3.3-70b |
| Paid | **OpenAI** | gpt-4o, gpt-4o-mini, gpt-3.5-turbo |
| Paid | **Anthropic** | claude-3-5-sonnet, claude-3-haiku |
| Paid | **Gemini Pro** | gemini-1.5-pro |

---

## Setup

**1. Clone and install dependencies**
```bash
git clone <repo-url>
cd llm_analyzer
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

**2. Configure API keys**
```bash
cp .env.example .env
```
Open `.env` and fill in the keys you have. Free-tier keys (Groq, Gemini, Cerebras) are available at no cost.

**3. Set your active tier**

In `.env`:
```env
ACTIVE_TIER=free    # "free" | "paid" | "all"
DEMO_MODE=true      # set false to use real API keys
```

**4. Launch the notebook**
```bash
jupyter lab llm_analyzer.ipynb
```

---

## Demo Mode

Set `DEMO_MODE=true` in `.env` to run the full benchmark with **simulated API responses** — no keys needed. Useful for exploring charts and output structure before wiring up real keys.

---

## Benchmark Tasks

The notebook tests each model against **13 prompts** across 5 task types:

| Task | Description |
|------|-------------|
| `summarization` | Summarize articles and technical concepts |
| `qa` | Factual question answering |
| `rag` | Answer questions from a provided context |
| `classification` | Sentiment, spam detection, language detection |
| `code_generation` | Python functions, SQL queries |

---

## Outputs

All outputs are saved to the `outputs/` folder after running the notebook:

| File | Description |
|------|-------------|
| `llm_benchmark_results.csv` | Full run-level data — every model/task/prompt combination |
| `llm_benchmark_summary.csv` | Model-level summary — accuracy, latency, cost, efficiency rank |
| `chart1_tokens.png` | Input vs output token usage per model |
| `chart2_latency.png` | Latency distribution box plot + heatmap by task |
| `chart3_cost.png` | Average cost per request and cost breakdown by task |
| `chart4_scatter.png` | Cost vs accuracy scatter (overall + per task) |
| `chart5_efficiency.png` | Efficiency score (accuracy / dollar) + multi-metric profile |
| `chart6_accuracy_heatmap.png` | Accuracy heatmap: model x task |
| `chart7_tier_comparison.png` | Free vs paid tier side-by-side comparison (when `ACTIVE_TIER=all`) |

---

## Project Structure

```
llm_analyzer/
├── llm_analyzer.ipynb          # Main benchmark notebook
├── requirements.txt            # Python dependencies
├── pyproject.toml              # Package metadata
├── .env                        # API keys (never committed)
├── .env.example                # Key template (safe to commit)
├── .gitignore
├── README.md
├── outputs/                    # Generated charts and CSVs
│   ├── llm_benchmark_results.csv
│   ├── llm_benchmark_summary.csv
│   └── chart*.png
└── src/
    └── llm_analyzer/
        └── __init__.py
```

---

## Free Tier API Key Links

| Provider | Sign-up |
|----------|---------|
| Groq | https://console.groq.com/keys |
| Google Gemini | https://aistudio.google.com/app/apikey |
| Cerebras | https://cloud.cerebras.ai |
