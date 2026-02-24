#  LLM Cost & Token Efficiency Analysis📊💹

> 📊 Benchmark 14 LLMs across Groq, Gemini, Cerebras, OpenAI, and Anthropic. Compare cost, latency, token usage, and accuracy — free-tier and paid-tier — all in one Jupyter notebook.

A data-driven benchmarking notebook that compares **14 LLMs across 5 providers** on cost, latency, token usage, and accuracy — with support for both free-tier and paid-tier API keys. Includes an advanced **RAG Chunk Size vs Cost Experiment** that reveals the optimal chunk size for balancing accuracy and token efficiency.

---

## 🌐 Providers Covered

| Tier | Provider | Models |
|------|----------|--------|
| Free | **Groq** | llama-3.1-8b-instant, llama-3.3-70b-versatile, llama-4-scout-17b, qwen3-32b |
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
<img width="2367" height="887" alt="chart1_tokens" src="https://github.com/user-attachments/assets/ad7fe973-94f7-4ca4-97cf-9f3b965ac6e0" />


#### `⏱️ Latency Analysis` — 
Box plot of latency distributions per model alongside a model x task heatmap showing average response times.
<img width="2619" height="886" alt="chart2_latency" src="https://github.com/user-attachments/assets/cb1e7f7f-7685-443c-9a77-f31c7a1ce363" />


#### `💰 Cost Analysis` — 
Horizontal bar chart of average cost per request by model (in µ$), plus a grouped bar breakdown of cost per task type per model.
<img width="2379" height="886" alt="chart3_cost" src="https://github.com/user-attachments/assets/01b02efd-1ab6-4bd5-8bb2-32b30ed9961b" />


#### `🏆 Efficiency Score` — 
Efficiency ranking (accuracy per dollar spent) and a normalized multi-metric profile chart comparing accuracy, speed, and cheapness side by side.
<img width="2376" height="888" alt="chart5_efficiency" src="https://github.com/user-attachments/assets/4797c24a-cb9c-4e39-b25b-c8b409e5a3f3" />


#### `⚖️ Cost vs Accuracy Trade-Off` — 
Scatter plot mapping each model by average cost vs average accuracy — overall view and per task type. Includes quadrant labels (Cheap+Accurate, Costly+Accurate, etc.).
<img width="2381" height="1035" alt="chart4_scatter" src="https://github.com/user-attachments/assets/823d88bf-0c7f-4733-9b86-8b8d87d9d0d1" />



#### `🎯 Accuracy Heatmap` — 
Color-coded heatmap of accuracy scores across every model x task combination. Green = high accuracy, red = low.
<img width="1672" height="739" alt="chart6_accuracy_heatmap" src="https://github.com/user-attachments/assets/0139d52f-c58f-49ec-ba6e-13fc3806d950" />


#### `🆓💳 Free vs Paid Tier Comparison` — 
Three-panel comparison: accuracy by model coloured by tier, latency by model, and an accuracy vs latency bubble chart (bubble size = cost).
<img width="2976" height="888" alt="chart7_tier_comparison" src="https://github.com/user-attachments/assets/71bcd53d-83c8-490d-8c5b-92a775a58be1" />


> **Note:** Chart 7 only renders when both free and paid models are present (i.e. `ACTIVE_TIER=all`).

#### `🔍 RAG Chunk Size Experiment` —
Three-panel chart from Section 7: input tokens vs chunk size (line per model), accuracy vs chunk size, and a cost vs accuracy bubble chart where bubble size represents chunk size. Identifies the most token-efficient chunk size — the sweet spot between context quality and token cost.

| Chunk Size | Effect |
|------------|--------|
| **200 tokens** | Lowest cost, risk of losing key context |
| **500 tokens** | Balanced — usually the optimal sweet spot |
| **1000 tokens** | Highest accuracy potential, highest cost |

<img width="2981" height="888" alt="chart8_rag_chunk_experiment" src="https://github.com/user-attachments/assets/59acf771-cb3f-41a5-ac3e-0708af81701e" />


---
