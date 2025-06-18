# T5-Base Finetuning
## By Victoria Lassner

## Overview
The goal of this project is to finetune a text summarization model efficiently using a T5 architecture with the CNN/DailyMail dataset. It transforms lengthy news articles into concise summaries while maintaining their core meaning most of the time.

## Data
- CNN/DailyMail dataset
- Composed of 300K news articles
- Three columns it has are ID, article and highlights.
- I used a random subset of 7000 examples from the dataset to train each round.
- I trained it for a total of four rounds.

## Models/Architectures
- T5-Base model with T5Tokenizer
- Training performed for 3 epochs with a batch size of 4, using Hugging Face's `Trainer`.

## Tools and Frameworks
- Hugging Face Transformers & Datasets
- PyTorch backend
- Evaluation using ROUGE scores

## How to run
- Create a virtual environment
- Download requirements.txt (may need to update certain packages)
- Run command: streamlit run app.py

## Results
- 'eval_rouge1': 42.85, 'eval_rouge2': 20.25, 'eval_rougeL': 30.46, 'eval_rougeLsum': 30.47
- Very close to original T5 paper of 43–44 ROUGE-1, 20–21 ROUGE-2, and 40+ ROUGE-L on CNN/Daily Mail considering restraints I worked within.
- Runtime: 33 minutes per session with 1.49 samples/sec with colab GPU.
- Runtime without GPU and only 3000 samples ~9 hours with 0.09 samples/sec.

## Next Steps
- Add more languages other than English.
- Use it to create study aids - use different dataset to add essays and such like Notebooklm.

## Model Artifacts
- I uploaded my model to HuggingFace after each session and continuously retrained it by pulling it back down from HuggingFace.
- I did use checkpoints at every 1000 steps as a fail safe in case colab timed out which occured often.

### Steps to retrain and save model
- model_T5 = "vlassner01/t5_cnn_model_base_v4"
- tokenizer = T5Tokenizer.from_pretrained(model_T5)
- model = T5ForConditionalGeneration.from_pretrained(model_T5)
### Load model and tokenizer
- model = T5ForConditionalGeneration.from_pretrained("/content/t5_cnn_model_base_v4")
- tokenizer = T5Tokenizer.from_pretrained("/content/t5_cnn_model_base_v4")

### Train the model . . .

### Save Locally
- model.save_pretrained("/content/t5_cnn_model_base_v4")
- tokenizer.save_pretrained("/content/t5_cnn_model_base_v4")

### Save to HuggingFace
- model.push_to_hub("vlassner01/t5_cnn_model_base_v4",  commit_message="Version_5")
- tokenizer.push_to_hub("vlassner01/t5_cnn_model_base_v4")

## Challenges
- Added padding so all sequences were the same length.
- Break the large dataset into chunks for easier computate rather than loading the whole dataset into memory.
- Saving the spiece.model file to HugginFace.
