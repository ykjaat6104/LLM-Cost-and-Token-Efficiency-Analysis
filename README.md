#  LLM Cost & Token Efficiency Analyzer📊💹

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
git clone https://github.com/ykjaat6104/LLM-Cost-and-Token-Efficiency-Analysis.git
cd LLM-Cost-and-Token-Efficiency-Analysis
python -m venv .venv
.venv\Scripts\activate        # Windows
source .venv/bin/activate     # Mac/Linux
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

The notebook tests each model against **12 prompts** across 5 task types:

| Task | Description |
|------|-------------|
| `summarization` | 📝 Summarize articles and technical concepts |
| `qa` | ❓ Factual question answering |
| `rag` | 🔍 Answer questions from a provided context |
| `classification` | 🏷️ Sentiment, spam detection, language detection |
| `code_generation` | 💻 Python functions, SQL queries |

---

## �️ DataFrame Structure

Every experiment run is recorded as a row in the results DataFrame — one row per **model × task × prompt** combination:

| Column | Type | Description |
|--------|------|-------------|
| `model` | str | Model display name e.g. `gemini-2.0-flash` |
| `provider` | str | API provider: `groq`, `gemini`, `cerebras`, `openai`, `anthropic` |
| `tier` | str | `free` or `paid` |
| `task` | str | Task type: `summarization`, `qa`, `rag`, `classification`, `code_generation` |
| `prompt_id` | int | Index of the prompt within its task |
| `input_tokens` | int | Tokens in the prompt sent to the model |
| `output_tokens` | int | Tokens in the model's response |
| `total_tokens` | int | `input_tokens + output_tokens` |
| `cost` | float | Request cost in USD (free-tier models = $0.00) |
| `latency` | float | Response time in seconds |
| `accuracy` | float | Score between 0.0–1.0 based on keyword/exact match |
| `cost_per_accuracy` | float | `cost / accuracy` — efficiency proxy |

> Each run produces **96 rows** in free-tier mode (8 models × 12 prompts) and **168 rows** in all-tier mode (14 models × 12 prompts). This structured format makes the data directly usable for further ML analysis, cost modelling, or custom visualizations.

---

## �🗂️ Project Structure

```
LLM-Cost-and-Token-Efficiency-Analysis/
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


## 📁 Outputs

All outputs are saved to the `outputs/` folder after running the notebook.

### 📄 Data Files

#### `llm_benchmark_results.csv`
Full run-level data — one row per model/task/prompt combination. Contains input tokens, output tokens, total tokens, cost, latency, and accuracy score for every single run.

#### `llm_benchmark_summary.csv`
Model-level aggregated summary — average accuracy, latency, cost per request, total spend, efficiency rank, and use-case recommendations grouped by model.

---

### 📈 Charts

#### `🪙 Token Usage Analysis` — 
Two-panel chart showing average input vs output token breakdown per model (grouped bar) and token distribution across task types (stacked bar).
<img width="2361" height="887" alt="chart1_tokens" src="https://github.com/user-attachments/assets/fadc0f05-bede-4646-939a-0655b4d928e0" />


#### `⏱️ Latency Analysis` — 
Box plot of latency distributions per model alongside a model x task heatmap showing average response times.
<img width="2619" height="886" alt="chart2_latency" src="https://github.com/user-attachments/assets/4c990406-65eb-423f-8028-536a1c810ab2" />


#### `💰 Cost Analysis` — 
Horizontal bar chart of average cost per request by model (in µ$), plus a grouped bar breakdown of cost per task type per model.
<img width="2379" height="886" alt="chart3_cost" src="https://github.com/user-attachments/assets/885ff42c-55de-448f-ae5a-7b3e6e464117" />


#### `🏆 Efficiency Score` — 
Efficiency ranking (accuracy per dollar spent) and a normalized multi-metric profile chart comparing accuracy, speed, and cheapness side by side.
<img width="2376" height="888" alt="chart5_efficiency" src="https://github.com/user-attachments/assets/445f58d5-5d21-4fc0-8f70-ad280e1661d2" />


#### `⚖️ Cost vs Accuracy Trade-Off` — 
Scatter plot mapping each model by average cost vs average accuracy — overall view and per task type. Includes quadrant labels (Cheap+Accurate, Costly+Accurate, etc.).
<img width="2380" height="1035" alt="chart4_scatter" src="https://github.com/user-attachments/assets/2f36614c-5e8f-4f6c-b453-e31a419fb111" />


#### `🎯 Accuracy Heatmap` — 
Color-coded heatmap of accuracy scores across every model x task combination. Green = high accuracy, red = low.
<img width="1672" height="739" alt="chart6_accuracy_heatmap" src="https://github.com/user-attachments/assets/26e1d89f-d533-4fa1-aecb-4da338cbe14d" />


#### `🆓💳 Free vs Paid Tier Comparison` — 
Three-panel comparison: accuracy by model coloured by tier, latency by model, and an accuracy vs latency bubble chart (bubble size = cost).
<img width="2977" height="888" alt="chart7_tier_comparison" src="https://github.com/user-attachments/assets/fee06337-39ad-47b0-af7d-d181f34368b6" />


---
