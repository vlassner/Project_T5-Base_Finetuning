# DSML 4220 Project

# Overview
The goal of this project is to learn how to train a text summarization model on a dataset for news articles and create a web app that allows the user to enter a url to get a summary of the news article.

# Data
The dataset I chose is the CNN / DailyMail dataset. It is composed of 300K news articles and their corresponding summary. The three columns it has are ID, article and highlights.

# Models/Architectures
I chose to use a pretrained T-5 base model with its corresponding T5Tokenizer to finetune it to do abstractive text summarization on news articles. I used a GPU to train the model since its average time without it was over eight hours. . . . .. . . . . .

# Tools and Frameworks
I used the HuggingFace Transformers package which included the the model, its tokenizer, training arguements and the trainer and dataset package which inlcuded the CNN/DailyMail dataset. Pytorch was used by the HuggingFace APIs.
