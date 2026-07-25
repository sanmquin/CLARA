# CLARA: Comprehension and Literacy Assessment for Readability Analysis

CLARA is a Python notebook-based tool for evaluating reading comprehension, with a specific focus on understanding why language models make mistakes. It utilizes a two-tier model framework to generate high-quality reading comprehension tasks and evaluate model capabilities through rigorous statistical analysis, prompt-based ablation studies, and comprehensive error categorization.

## Features

1. **Fictitious Story & Question Generation (Gemini 2.5/1.5 Flash)**
   - Generates a completely novel, fictitious story.
   - Creates multiple-choice questions (options A, B, C, D) categorized into three difficulty levels: **Easy**, **Medium**, and **Hard**.
   - Outputs structured JSON to guarantee reliable question processing.

2. **Multi-Trial Question Answering (GPT-2 Model Family)**
   - Downloads model weights directly inside the notebook (no training or fine-tuning required).
   - Evaluates a configurable number of trials (10 to 50 times per question) using temperature sampling.
   - Formats the inputs with story context, target question, option keys, and answer prompts.
   - Validates generated strings, automatically filtering and discarding any answers that do not conform to the expected multiple-choice format (e.g., must resolve to option letter A, B, C, or D).

3. **Ablation Studies & Model Scale Analysis**
   - Configurable ablation settings to compare different sizes of the GPT-2 family: `gpt2` (small), `gpt2-medium` (medium), `gpt2-large` (large), and `gpt2-xl` (xl).
   - Automatically tracks accuracy and parses failures across all specified models.

4. **Detailed Error Analysis & Visualizations**
   - Calculates overall accuracy and accuracy segmented by question difficulty.
   - Identifies specific questions that prompt-level models consistently fail to answer correctly.
   - Generates plots comparing performance across models and difficulty tiers.

5. **Google Drive Integration & Persistent Caching**
   - Runs seamlessly in Google Colab.
   - Persistently caches all outputs (Gemini-generated stories/questions and GPT-2 simulation results) in Google Drive under:
     - `/content/drive/MyDrive/clara_cache/story_questions.json`
     - `/content/drive/MyDrive/clara_cache/gpt2_results_<model_name>_<runs>.json`
   - Includes automatic local fallback (`./clara_cache/`) if Google Drive is not mounted.

---

## Google Drive Cache Directory Structure

To optimize costs and run repeatable experiments, outputs are saved at the following paths:

* **Story and Questions Cache**:
  - Google Drive: `/content/drive/MyDrive/clara_cache/story_questions.json`
  - Local Fallback: `./clara_cache/story_questions.json`
* **GPT-2 Simulation Results Cache**:
  - Google Drive: `/content/drive/MyDrive/clara_cache/gpt2_results_<model_name>_<runs>.json`
  - Local Fallback: `./clara_cache/gpt2_results_<model_name>_<runs>.json`

---

## Getting Started in Google Colab

1. **Open the Notebook**
   - Upload the `clara_evaluation.ipynb` notebook to Google Colab.
2. **Mount Google Drive** (Optional but highly recommended for persistent caching)
   - Follow the prompt in Cell 1 to authorize Google Drive access.
3. **Configure Parameters**
   - Input your Gemini API key in the configuration cell.
   - Adjust parameters like the list of ablation models, the number of run trials (10-50), and temperatures.
4. **Run All Cells**
   - Execution will automatically generate stories (or load from cache), evaluate the GPT-2 models (or load previous trial runs), and generate rich analysis plots.

---

## File Contents

- `clara_evaluation.ipynb`: The main Colab-compatible notebook, featuring highly documented markdown titles and descriptions for every cell.
- `AGENTS.md`: Instruction guide for AI agents and developer contributors.
- `README.md`: Project description, architecture details, and usage guide.
