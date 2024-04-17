# Sentiment Analysis of Customer Feedback

## Background
In today’s digital era, diverse channels such as social media platforms, emails, and customer surveys are being used to provide customer feedback. This has made it a challenge for our orgnanisation to efficiently and accurately analyse the feedback, which is crucial in enabling data-driven decision-making for the company.

This project aims to provide our organisation with an easy and methodical way of analysing customer feedback, and in so doing, enhance customer understanding, improve service quality, and enable data-driven decision-making. To overcome the shortfalls of manual sorting which is time-consuming and error-prone, this project leverages NLP techniques to gauge customer sentiment, identify trends, and highlight areas for improvements.

## Data Scraping
Data scraping for this project was carried out in March 2024. Data was obtained from various banking apps on the Apple Store and Google Play Store. Relevant information such as ratings, comments, replies, and thumbs up counts were retained. Other information that contained personal information or were not useful were discarded. The code used for data scraping can be found in [dataset.py](dataset.py). The final dataset was subsequently uploaded to an SQL database for easier access and retrieval.

## Model Description
The code for model training and testing can be found [here](modeltrainingandtests.py).

### Sentiment Analysis
We performed sentiment analysis using a fine-tuned HuggingFace model. For the labels, we used the star ratings collected, classifying reviews with 4 or 5 stars as 'positive' and the rest as 'negative'.

### Intent Extraction
To extract intent from reviews, we tried a few different methods: text summarisation, topic modelling, and keyword extraction using KeyBERT and rake-nltk. We found that text summarisation did not work well as the reviews were too short, while topic modelling was not feasible as we did not have a predefined topic list that was comprehensive enough. In the end, the keyBERT model was used for intent extraction.

### Summarising Sentiment and Intent
We used a net sentiment figure as a summary of overall sentiment. The net sentiment was used as an alternative to the Net Promoter Score (NPS) as we did not have data specific to the NPS. This metric was referenced from the following [website](https://chattermill.com/blog/nps-calculator#:~:text=Calculating%20your%20net%20promoter%20score,number%20between%20%2D100%20and%20100.).
To summarise overall intent, two dictionaries containing intents associated with positive and negative sentiment reviews respectively. These dictionaries are sorted in descending frequency of keywords.

## GPT
As an extension to our project, we wanted to create a language model that was able to generate replies to reviews. For this, the causal language model from HuggingFace was used, with the baseline model 'openai-community/gpt2'. The code for the finetuning of the GPT can be found [here](gpt_finetune_causallm.ipynb).
