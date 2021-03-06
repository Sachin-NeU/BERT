# BERT

BERT (Bidirectional Encoder Representations from Transformers) is a paper published by researchers at Google AI Language in October 2018. It has caused a stir in the Machine Learning community by presenting state-of-the-art results in a wide variety of NLP tasks, including Question Answering (SQuAD v1.1), Natural Language Inference (MNLI), and others. On December 9, 2019, it was reported that BERT had been adopted by Google Search for over 70 languages.

Google CLaat link: https://docs.google.com/document/d/1NwOshs-3_eBvzpP8XHsfYtCtRZhMleKM07xXQqawpwI/edit#

## Setup

**Using Colab GPU for Training**

Google Colab offers free GPUs and TPUs! Since we’ll be training a large neural network it’s best to run this ipynb file in Google Colab GPUs.

## Installing the Hugging Face Library

Install the transformers package from Hugging Face which will give us a pytorch interface for working with BERT. 

`!pip install transformers`

## Download CoLA dataset

We’ll use The Corpus of Linguistic Acceptability (CoLA) dataset for single sentence classification. It’s a set of sentences labeled as grammatically correct or incorrect. It was first published in May of 2018, and is one of the tests included in the “GLUE Benchmark” on which models like BERT are competing. The dataset is hosted on GitHub in this repo: https://nyu-mll.github.io/CoLA/

We’ll use the wget package to download the dataset to the Colab instance’s file system.

`!pip install wget`

