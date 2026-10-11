# 🤖 My AI Learning Journey

A personal home base for learning AI: projects, coding practice, new skills, and notes.
I'm a beginner, so this repo is about **steady progress**, not perfection.

---

## 🎯 Goals

- Understand the basics of machine learning and generative AI
- Build small, real AI projects (chatbots, agents, simple models)
- Get comfortable with Python, Git, and GitHub
- Make my **first open-source contribution** to an AI project

## 🗂️ How this repo is organized

| Folder | What goes in it |
| --- | --- |
| `projects/` | Small AI projects I build (one folder per project) |
| `notes/` | What I learned from courses, videos, and articles |
| `skills/` | Practice exercises (Python, prompts, Git, etc.) |
| `contributions/` | Notes on open-source PRs/issues I worked on |

> Folders get created as I add things to them.

## 📅 Learning log

| Date | Topic | What I did | Link |
| --- | --- | --- | --- |
| 2026-10-11 | Getting started | Created this repo and picked repos to follow | — |

---

## ⭐ Repos I'm following (beginner-friendly + trending)

Star counts as of Oct 2026. **Start at the top and work down.**

### Step 0 — Practice making a contribution (not AI, but the best first step)

| Repo | Why |
| --- | --- |
| [firstcontributions/first-contributions](https://github.com/firstcontributions/first-contributions) | Step-by-step guide to your very first pull request. Do this first! |

### 📚 Courses: learn the concepts

| # | Repo | ⭐ | Why it's great for beginners |
| --- | --- | --- | --- |
| 1 | [microsoft/generative-ai-for-beginners](https://github.com/microsoft/generative-ai-for-beginners) | 121k | 21 lessons on building with generative AI. Best starting point. |
| 2 | [microsoft/ML-For-Beginners](https://github.com/microsoft/ML-For-Beginners) | 91k | 12-week classic machine learning course with quizzes |
| 3 | [microsoft/AI-For-Beginners](https://github.com/microsoft/AI-For-Beginners) | 70k | 12-week overview of AI: neural nets, vision, NLP |
| 4 | [microsoft/ai-agents-for-beginners](https://github.com/microsoft/ai-agents-for-beginners) | 77k | 18 lessons on AI agents, the hottest topic right now |
| 5 | [huggingface/agents-course](https://github.com/huggingface/agents-course) | 33k | Free Hugging Face course on agents, with a certificate |
| 6 | [mlabonne/llm-course](https://github.com/mlabonne/llm-course) | 83k | LLM roadmap plus free Colab notebooks (no install needed) |
| 7 | [rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) | 106k | Build a mini ChatGPT step by step to see how LLMs work |
| 8 | [dair-ai/Prompt-Engineering-Guide](https://github.com/dair-ai/Prompt-Engineering-Guide) | 79k | Prompting, RAG, and agents explained clearly |

### 🍳 Cookbooks: copy-paste examples

| # | Repo | ⭐ | Why |
| --- | --- | --- | --- |
| 9 | [openai/openai-cookbook](https://github.com/openai/openai-cookbook) | 77k | Ready-to-run examples using the OpenAI API |
| 10 | [anthropics/claude-cookbooks](https://github.com/anthropics/claude-cookbooks) | 53k | Ready-to-run examples using Claude |

### 🛠️ Tools: run and build AI yourself

| # | Repo | ⭐ | Why |
| --- | --- | --- | --- |
| 11 | [ollama/ollama](https://github.com/ollama/ollama) | 183k | Run AI models on your own computer with one command |
| 12 | [open-webui/open-webui](https://github.com/open-webui/open-webui) | 154k | A ChatGPT-style web app for your local models |
| 13 | [gradio-app/gradio](https://github.com/gradio-app/gradio) | 44k | Turn Python code into a web demo in a few lines. Very welcoming community. |
| 14 | [huggingface/transformers](https://github.com/huggingface/transformers) | 167k | The standard library for AI models. Has many "good first issue" labels. |
| 15 | [huggingface/smolagents](https://github.com/huggingface/smolagents) | 30k | Small, readable agent library, good to learn from |
| 16 | [langchain-ai/langchain](https://github.com/langchain-ai/langchain) | 148k | Popular framework for LLM apps and agents |
| 17 | [run-llama/llama_index](https://github.com/run-llama/llama_index) | 52k | Connect LLMs to your own documents (RAG) |
| 18 | [crewAIInc/crewAI](https://github.com/crewAIInc/crewAI) | 60k | Make teams of AI agents work together |
| 19 | [modelcontextprotocol/servers](https://github.com/modelcontextprotocol/servers) | 91k | MCP lets AI tools connect to apps. Lots of small examples. |
| 20 | [scikit-learn/scikit-learn](https://github.com/scikit-learn/scikit-learn) | 68k | Classic ML in Python with excellent docs. Docs fixes are great first PRs. |

### ⚡ Star + watch them all at once

Install the [GitHub CLI](https://cli.github.com/), run `gh auth login`, then:

```bash
for r in \
  firstcontributions/first-contributions \
  microsoft/generative-ai-for-beginners microsoft/ML-For-Beginners \
  microsoft/AI-For-Beginners microsoft/ai-agents-for-beginners \
  huggingface/agents-course mlabonne/llm-course rasbt/LLMs-from-scratch \
  dair-ai/Prompt-Engineering-Guide openai/openai-cookbook \
  anthropics/claude-cookbooks ollama/ollama open-webui/open-webui \
  gradio-app/gradio huggingface/transformers huggingface/smolagents \
  langchain-ai/langchain run-llama/llama_index crewAIInc/crewAI \
  modelcontextprotocol/servers scikit-learn/scikit-learn; do
  gh api -X PUT "user/starred/$r" --silent && echo "⭐ starred $r"
  gh api -X PUT "repos/$r/subscription" -F subscribed=true --silent && echo "👀 watching $r"
done
```

> 💡 **Watching tip:** "Watching" big repos like `transformers` sends *hundreds* of emails a day.
> For most repos, choose **Watch → Custom → Releases** on the repo page instead.
> Only fully watch the 2–3 repos you want to contribute to.

---

## 🧭 How to find your first contribution

1. Finish [first-contributions](https://github.com/firstcontributions/first-contributions) to practice the fork → branch → PR flow.
2. In any repo above, open **Issues** and filter by labels like
   `good first issue`, `help wanted`, `documentation`, or `hacktoberfest` (it's October!).
3. Start with **typo fixes, docs improvements, or translations**. These count and are welcome.
4. Leave a comment asking to work on an issue before starting.
5. Log what you did in the `contributions/` folder here.

Handy search: [good first issues in AI repos](https://github.com/search?q=label%3A%22good+first+issue%22+topic%3Allm+state%3Aopen&type=issues)
