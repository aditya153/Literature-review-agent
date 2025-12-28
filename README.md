# 📚 Literature Review Agent

A **Multi-Agent System** for automatically generating comprehensive literature reviews from research papers using AI-powered agents.

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)
![AutoGen](https://img.shields.io/badge/AutoGen-0.10-green)
![Groq](https://img.shields.io/badge/Groq-LLaMA--4-purple)
![License](https://img.shields.io/badge/License-MIT-yellow)

## 🎯 Overview

This project leverages a **multi-agent architecture** powered by Microsoft's AutoGen framework to automate the process of creating literature reviews. It processes multiple PDF research papers, extracts key information, and generates cohesive, well-structured literature reviews with built-in quality evaluation using ROUGE metrics.

## ✨ Key Features

- 🤖 **Multi-Agent Collaboration** - Specialized AI agents work together for summarization, review generation, and evaluation
- 📄 **PDF Processing** - Automatic text extraction from research papers using PyMuPDF
- 🧠 **LLM-Powered Analysis** - Uses Groq's LLaMA-4 model for intelligent text processing
- 📊 **Quality Metrics** - ROUGE score evaluation for literature review quality assessment
- 🔄 **Interactive Refinement** - Human-in-the-loop capability for review improvement
- 📝 **Section Detection** - Smart extraction of abstracts, introductions, and methodology sections

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                        LITERATURE REVIEW AGENT SYSTEM                        │
└─────────────────────────────────────────────────────────────────────────────┘

                              ┌─────────────────┐
                              │   User Input    │
                              │  (PDF Papers)   │
                              └────────┬────────┘
                                       │
                                       ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                           PDF PROCESSING LAYER                               │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐          │
│  │  PyMuPDF        │───▶│ Text Extraction │───▶│ Section Parser  │          │
│  │  Document       │    │  (Full Text)    │    │ (Abstract,      │          │
│  │  Reader         │    │                 │    │  Introduction,  │          │
│  └─────────────────┘    └─────────────────┘    │  Methodology)   │          │
│                                                 └────────┬────────┘          │
└─────────────────────────────────────────────────────────│────────────────────┘
                                                          │
                                                          ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                         MULTI-AGENT ORCHESTRATION                            │
│                         (AutoGen Framework)                                  │
│                                                                              │
│  ┌──────────────────────────────────────────────────────────────────────┐   │
│  │                      Group Chat Manager                               │   │
│  │               (CustomGroupChatManager)                                │   │
│  └──────────────────────────────────────────────────────────────────────┘   │
│                                    │                                         │
│           ┌────────────────────────┼────────────────────────┐               │
│           │                        │                        │               │
│           ▼                        ▼                        ▼               │
│  ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐         │
│  │   Summarizer    │    │    Reviewer     │    │     Human       │         │
│  │     Agent       │    │     Agent       │    │  UserProxy      │         │
│  │                 │    │                 │    │     Agent       │         │
│  │ • Extract key   │    │ • Generate      │    │ • Interactive   │         │
│  │   contributions │    │   cohesive      │    │   feedback      │         │
│  │ • Methodology   │    │   500-word      │    │ • Revise/       │         │
│  │ • Technical     │    │   literature    │    │   Refine        │         │
│  │   details       │    │   review        │    │   commands      │         │
│  │ • Novel aspects │    │                 │    │                 │         │
│  └────────┬────────┘    └────────┬────────┘    └────────┬────────┘         │
│           │                      │                      │                   │
│           └──────────────────────┴──────────────────────┘                   │
│                                  │                                          │
│                                  ▼                                          │
│                      ┌─────────────────────┐                                │
│                      │  Evaluator Agent    │                                │
│                      │ (Enhanced Eval)     │                                │
│                      │                     │                                │
│                      │ • ROUGE-1 F1 Score  │                                │
│                      │ • ROUGE-L F1 Score  │                                │
│                      └─────────────────────┘                                │
└─────────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
┌─────────────────────────────────────────────────────────────────────────────┐
│                              LLM BACKEND                                     │
│                                                                              │
│                    ┌─────────────────────────────────┐                      │
│                    │         Groq API                │                      │
│                    │  (OpenAI-compatible endpoint)   │                      │
│                    │                                 │                      │
│                    │  Model: LLaMA-4-Scout-17B       │                      │
│                    │  Temperature: 0.3               │                      │
│                    │  Max Tokens: 1000               │                      │
│                    └─────────────────────────────────┘                      │
└─────────────────────────────────────────────────────────────────────────────┘
                                       │
                                       ▼
                              ┌─────────────────┐
                              │    Output       │
                              │  Literature     │
                              │    Review       │
                              └─────────────────┘
```

## 🔄 Workflow Diagram

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Upload    │────▶│   Extract   │────▶│  Summarize  │────▶│   Review    │
│  PDFs (6+)  │     │    Text     │     │   Papers    │     │ Generation  │
└─────────────┘     └─────────────┘     └─────────────┘     └──────┬──────┘
                                                                    │
                                                                    ▼
                                        ┌───────────────────────────────────┐
                                        │        Interactive Loop           │
                                        │  ┌─────────────────────────────┐  │
                                        │  │  evaluate - ROUGE scoring   │  │
                                        │  │  revise - Refine review     │  │
                                        │  │  exit - Complete session    │  │
                                        │  └─────────────────────────────┘  │
                                        └───────────────────────────────────┘
```

## 🛠️ Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| **Agent Framework** | AutoGen (AG2) | Multi-agent orchestration and conversation management |
| **LLM Backend** | Groq API | Fast inference with LLaMA-4-Scout-17B model |
| **PDF Processing** | PyMuPDF (fitz) | Extract text from research paper PDFs |
| **Evaluation** | ROUGE | Quality assessment of generated reviews |
| **Runtime** | Google Colab | GPU-accelerated notebook environment |
| **Language** | Python 3.9+ | Core programming language |

## 📂 Project Structure

```
Literature-review-agent/
├── multi_agent_system_for_creating_literature_reviews.ipynb   # Main notebook
├── Research Paper for Multi-agent System.pdf                  # Reference paper
└── README.md                                                    # Documentation
```

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- Groq API key
- Google Colab (recommended) or Jupyter environment

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/aditya153/Literature-review-agent.git
   cd Literature-review-agent
   ```

2. **Install dependencies:**
   ```bash
   pip install pymupdf autogen rouge groq
   ```

3. **Configure API key:**
   ```python
   import os
   os.environ["OPENAI_API_KEY"] = "your-groq-api-key"
   os.environ["OPENAI_BASE_URL"] = "https://api.groq.com/openai/v1"
   ```

### Usage

1. **Run the notebook** in Google Colab or Jupyter
2. **Upload at least 6 PDF research papers** when prompted
3. **Review the generated summaries** for each paper
4. **Interact with the system:**
   - `evaluate` - Compare your review with system output using ROUGE scores
   - `revise` - Request refinements to the literature review
   - `exit` - Complete the session

## 🤖 Agent Descriptions

### Summarizer Agent
Extracts structured technical information from each paper:
- Key contributions
- Methodology details
- Technical specifications
- Novel aspects and innovations

### Reviewer Agent
Generates a cohesive 500-word literature review synthesizing all paper summaries into a comprehensive academic narrative.

### Human UserProxy Agent
Enables human-in-the-loop interaction for:
- Reviewing generated content
- Requesting revisions
- Providing feedback

### Evaluator Agent
Calculates ROUGE metrics to assess review quality:
- **ROUGE-1 F1**: Unigram overlap score
- **ROUGE-L F1**: Longest common subsequence score

## 📊 Sample Output

```
Processing paper 1/6
[Summarizer Agent]: Technical Summary - Paper_Name.pdf:

**Key Contributions:**
1. Introduces novel prompt engineering framework...

**Methodology:**
1. Utilizes transformer-based learning systems...

---

[Reviewer Agent - Generated Literature Review]:
The rapidly evolving field of artificial intelligence...

---

ROUGE-1 F1: 96.4%
ROUGE-L F1: 96.4%
```

## 🔧 Configuration

Customize the LLM configuration in the notebook:

```python
llm_config = {
    "config_list": [{
        "model": "meta-llama/llama-4-scout-17b-16e-instruct",
        "temperature": 0.3,  # Lower = more focused output
        "max_tokens": 1000   # Adjust for longer/shorter responses
    }]
}
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under ME.

## 🙏 Acknowledgements

- [Microsoft AutoGen](https://github.com/microsoft/autogen) - Multi-agent framework
- [Groq](https://groq.com/) - Fast LLM inference
- [PyMuPDF](https://pymupdf.readthedocs.io/) - PDF processing library
- [ROUGE](https://github.com/pltrdy/rouge) - Evaluation metrics

---

<p align="center">
  Made with ❤️ for the research community
</p>
