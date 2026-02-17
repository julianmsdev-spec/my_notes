## What is an LLM?
An LLM is a neural network designed to understand, generate, and respond to human like text. 
LLMs utilize an architecture called the *transformer*, which allows them to pay selective attention to different parts of the input when making predictions, making them especially adept at handling the nuances and complexities of human language. 
Since LLMs are capable of *generating* text, LLMs are also often referred to as a form of generative artificial intelligence, often abbreviated as *generative AI* or *GenAI*. 

## Applications of LLMS
- Machine translation
- generation of novel texts
- sentiment analysis
- text summarization
- content creation 
- Chatbots and virtual assistants
- knowlege retrieval 

## Stages of building and using LLMs
The first step in creating an LLM is to train on a large corpus of text data, sometimes referred to as *raw* text. *raw* refers to the fact that this data is just regular text without any labeling information. The first training stage of the LLM is also known as *pretraining*, creating an initial pretrained LLM, often called a *base* or *foundation model*.
After obtaining a pretrained LLM from training on large text datasets, where the LLM is trained to predict the next word in the text, we can further train the LLM on labeled data, also known as *fine-tuning*.
The two most popular categories of fine-tuning LLMs are *instruction fine-tuning* and *classification fine-tuning*. 

## Introducing the transformer architecture
Most modern LLMs rely on the *transformer* architecture, which is a deep neural net-work architecture introduced in the 2017 paper "Attention is All You Need".
The transformer architecture consists of two submodules: an encoder and a decoder. The encoder module processes the input text and encodes it into a series of numerical representations or vectors that capture the contextual information of the input. Then, the decoder module takes these encoded vectors and generates the output text. In a translation task, for example the encoder would encode the text from the source language into vectors, and the decoder would decode these vectors to generate text in the target language. Both the encoder and decoder consists of many layers connected by a so-called self-attention mechanism. 