# Capstone Project: Do LLMs Know What/Where and Why They Lack?

This codebase was developed as a part of Bachelor’s capstone project in Data Science at American University of Armenia.

The project evaluates the self-refinement abilities of large language models (LLMs) by:
- Solving math questions
- Identifying incorrect answers
- Generating hint sentences given the correct answer
- Re-solving the questions with injected hints
- Measuring the improvement in accuracy

## Project Structure

your_project/  
├── data/  
│   ├── asdiv.jsonl           # ASDiv benchmark samples  
│   └── gsm8k.jsonl           # GSM8K benchmark samples  
├── prompts/  
│   ├── answer_prompt.txt     # Template for answer inference  
│   └── hint_prompt.txt       # Template for hint generation  
├── results/  
│   ├── gemma-2-2b-it/        # Outputs for model “gemma-2-2b-it”  
│   │   ├── initial_inference.jsonl  
│   │   ├── hints.jsonl  
│   │   └── post_hint_inference.jsonl  
│   ├── phi-4-mini-instruct/  # Same outputs for “phi-4-mini-instruct”  
│   └── statistics.txt        # Aggregated stats (after analysis step)  
├── src/  
│   ├── data.py               # load/save JSONL utilities  
│   ├── utils.py              # prompt builders & extraction helpers  
│   ├── inference.py          # solve_questions & generate_hints  
│   ├── run.py                # main pipeline CLI  
│   └── analysis.py           # compute & format summary stats  
├── README.md                 # Project overview and instructions  
└── requirements.txt          # Python dependencies  

## How to Use

1. Install dependencies:

```
pip install -r requirements.txt
```

2. Run the full pipeline

This will generate initial answers, hints, and post-hint answers:

```
python src/run.py \
  --model_path <HF-model-or-local-dir> \
  --input_path data/asdiv.jsonl \
  --output_dir results/gemma-2-2b-it \
  [--max_samples N]
```

- **--model_path**: Hugging Face checkpoint (e.g. `google/gemma-2-2b-it`) or local directory  
- **--input_path**: JSONL file with each line `{ "question": "...", "answer": "..." }`  
- **--output_dir**: Directory for three output files  
- **--max_samples** (optional): limit number of examples processed  

After running, you’ll find:

- `initial_inference.jsonl`  
- `hints.jsonl`  
- `post_hint_inference.jsonl`  

3. Analyze accuracy improvements

Summarize initial vs. post-hint accuracy across all model/dataset folders:

```
python src/statistics.py \
  --parent_dir results \
  --output_file results/statistics.txt
```

After running, you’ll find `statistics.txt` containing all evaluation metrics.
