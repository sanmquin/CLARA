# CLARA Agent Instructions (AGENTS.md)

Welcome, fellow agent! This file contains instructions, tips, and guidelines for working with the **CLARA** (Comprehension and Literacy Assessment for Readability Analysis) repository.

## Repository Structure
- `clara_evaluation.ipynb`: The main Google Colab-compatible Jupyter notebook.
- `README.md`: The main documentation for the repository.
- `AGENTS.md`: This instruction file for agents.

## Project Architecture & Methodology
CLARA is designed to evaluate reading comprehension in smaller language models and perform error analysis to understand why they fail.
1. **Story and Question Generation**: A Gemini Flash model generates a fictitious story and a structured list of reading comprehension questions. The questions are categorized into three difficulty levels: Easy, Medium, and Hard.
2. **Evaluation**: A GPT-2 family model (e.g., small, medium, large, xl) runs on the story and questions inside the Colab notebook. For each question, it generates predictions 10-50 times (configurable). The outputs must match a strict formatting schema; any answers that do not conform are discarded.
3. **Ablation & Analysis**: An ablation study compares performance across different sizes of the GPT-2 model family. Detailed statistical error analysis and visualizations are performed to identify where models struggle.
4. **Caching**: To reduce API costs and improve repeatability, all outputs from both Gemini and GPT-2 are cached in Google Drive (`/content/drive/MyDrive/clara_cache/`).

## Coding Conventions & Guidelines for the Notebook
- **Title and Description**: Each notebook cell **must** start with a Markdown header title (e.g., `### Cell 1: Environment Setup`) and include a copious, detailed description explaining its inputs, processing logic, outputs, and purpose.
- **Fail-Safe Caching**: Since Google Drive is only available when run in Colab, the code must support a fallback to a local cache directory `./clara_cache/` if Google Drive is not mounted or available.
- **Structured JSON Output**: When requesting stories and questions from Gemini, use Gemini's structured outputs (`response_schema`) or detailed prompt instructions to ensure they are parsed as clean JSON.
- **Answer Parsing Robustness**: The GPT-2 generation loop should check for common output patterns (e.g., `Answer: A`, `Answer: [A]`, or single letter outputs `A`, `B`, `C`, `D`) and cleanly parse them. Any generated responses that are completely malformed must be safely ignored/discarded from the scoring pool.

## Verification Instructions
Whenever you make changes to the notebook, run a syntax verification script:
```bash
python3 -c "import json; json.load(open('clara_evaluation.ipynb'))"
```
This ensures the notebook remains a valid, parseable JSON file.
