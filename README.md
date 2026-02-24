# 🤖 LLM Cost & Token Efficiency Analyzer

> 📊 Benchmark 14 LLMs across Groq, Gemini, Cerebras, OpenAI, and Anthropic. Compare cost, latency, token usage, and accuracy — free-tier and paid-tier — all in one Jupyter notebook.

A data-driven benchmarking notebook that compares **14 LLMs across 5 providers** on cost, latency, token usage, and accuracy — with support for both free-tier and paid-tier API keys.

---

## 🌐 Providers Covered

| Tier | Provider | Models |
|------|----------|--------|
| Free | **Groq** | llama-3.1-8b-instant, llama-3.3-70b-versatile, mixtral-8x7b-32768, gemma2-9b-it |
| Free | **Google Gemini** | gemini-1.5-flash, gemini-2.0-flash-exp |
| Free | **Cerebras** | llama3.1-8b, llama3.3-70b |
| Paid | **OpenAI** | gpt-4o, gpt-4o-mini, gpt-3.5-turbo |
| Paid | **Anthropic** | claude-3-5-sonnet, claude-3-haiku |
| Paid | **Gemini Pro** | gemini-1.5-pro |

---

## ⚙️ Setup

**1. Clone and install dependencies**
```bash
git clone <repo-url>
cd llm_analyzer
python -m venv .venv
.venv\Scripts\activate        # Windows
pip install -r requirements.txt
```

**2. 🔑 Configure API keys**
```bash
cp .env.example .env
```
Open `.env` and fill in the keys you have. Free-tier keys (Groq, Gemini, Cerebras) are available at no cost.

**3. 🎚️ Set your active tier**

In `.env`:
```env
ACTIVE_TIER=free    # "free" | "paid" | "all"
```

**4. 🚀 Launch the notebook**
```bash
jupyter lab llm_analyzer.ipynb
```

---

## 🧪 Benchmark Tasks

The notebook tests each model against **13 prompts** across 5 task types:

| Task | Description |
|------|-------------|
| `summarization` | 📝 Summarize articles and technical concepts |
| `qa` | ❓ Factual question answering |
| `rag` | 🔍 Answer questions from a provided context |
| `classification` | 🏷️ Sentiment, spam detection, language detection |
| `code_generation` | 💻 Python functions, SQL queries |

---

## 📁 Outputs

All outputs are saved to the `outputs/` folder after running the notebook.

### 📄 Data Files

#### `llm_benchmark_results.csv`
Full run-level data — one row per model/task/prompt combination. Contains input tokens, output tokens, total tokens, cost, latency, and accuracy score for every single run.

#### `llm_benchmark_summary.csv`
Model-level aggregated summary — average accuracy, latency, cost per request, total spend, efficiency rank, and use-case recommendations grouped by model.

---

### 📈 Charts

#### `chart1_tokens.png` — 🪙 Token Usage Analysis
Two-panel chart showing average input vs output token breakdown per model (grouped bar) and token distribution across task types (stacked bar).

#### `chart2_latency.png` — ⏱️ Latency Analysis
Box plot of latency distributions per model alongside a model x task heatmap showing average response times.

#### `chart3_cost.png` — 💰 Cost Analysis
Horizontal bar chart of average cost per request per model (in micro-dollars) and a grouped bar breakdown of cost per task type.

#### `chart4_scatter.png` — ⚖️ Cost vs Accuracy Trade-Off
Scatter plot mapping each model by average cost vs average accuracy — overall view and per task type. Includes quadrant labels (Cheap+Accurate, Costly+Accurate, etc.).

#### `chart5_efficiency.png` — 🏆 Efficiency Score
Efficiency ranking (accuracy per dollar spent) and a normalized multi-metric profile chart comparing accuracy, speed, and cheapness side by side.

#### `chart6_accuracy_heatmap.png` — 🎯 Accuracy Heatmap
Color-coded heatmap of accuracy scores across every model x task combination. Green = high accuracy, red = low.

#### `chart7_tier_comparison.png` — 🆓 vs 💳 Free vs Paid Tier Comparison
Three-panel comparison: accuracy ranking, latency ranking, and an accuracy-vs-latency bubble scatter (bubble size = cost). Only rendered when `ACTIVE_TIER=all`.

---

## 🗂️ Project Structure

```
llm_analyzer/
├── llm_analyzer.ipynb          # 📓 Main benchmark notebook
├── requirements.txt            # 📦 Python dependencies
├── pyproject.toml              # 🔧 Package metadata
├── .env.example                # 🔑 Key env template
├── .gitignore
├── README.md
└── src/
    └── llm_analyzer/
        └── __init__.py
```

