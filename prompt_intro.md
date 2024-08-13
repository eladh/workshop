# Prompt Engineering

[Overview](#overview)

## Overview

Prompt engineering is an emerging discipline focused on developing optimized prompts to efficiently apply language models to various tasks. Prompt engineering helps researchers understand the abilities and limits of large language models (LLMs). By using various prompt engineering techniques, you can often get better answers from the foundation models without spending effort and cost on retraining or fine-tuning them.

Note that prompt engineering does not involve fine-tuning the model. In fine-tuning, the weights/parameters are adjusted using training data with the goal of optimizing a cost function. Model fine-tuning is generally an expensive process in terms of computation time and actual costs. Prompt engineering attempts to guide the trained foundation model (FM) to provide more relevant and accurate answers using various methods, such as, better worded questions, similar examples, intermediate steps, and logical reasoning.

Prompt Engineering leverages the principle of \'93priming\'94: providing the model with a context of few (3-5) examples of what the user expects the output to look like, so that the model mimics the previously \'93primed\'94 behavior. By interacting with the LLM through a series of questions, statements, or instructions, users can effectively guide the LLM's understanding and adjust its behavior according to the specific context of the conversation.

In short, prompt engineering is a new and important field for optimizing how you apply, develop, and understand language models, especially large language models. At its core, it is about designing prompts and interactions to expand what language technologies can do, address their weaknesses, and gain insights into their functioning. Prompt engineering equips us with strategies and techniques for pushing the boundaries of what is possible with language models and their applications.

[Why is it relevant?](#why-is-it-relevant)

## Why is it relevant?

The key ideas are:

- Prompt engineering is the fastest way to harness the power of large language models.

- Prompt engineering optimizes how you work with and direct language models.

- It boosts abilities, improves safety, and provides understanding.

- Prompt engineering incorporates various skills for interfacing with and advancing language models.

- Prompt engineering enables new features like augmenting domain knowledge with language models without changing model parameters or fine-tuning.

- Prompt engineering provides methods for interacting with, building with, and grasping language models' capabilities.

- Higher quality prompt inputs lead to higher quality outputs.

In this guide, you will focus on best practices for prompt engineering with several models in Bedrock, including Amazon Titan models and third party models provided by Anthropic and Mistral AI.

[Structure of a prompt](#structure-of-a-prompt)

## Structure of a prompt

As you explore prompt engineering examples, note that each prompt contains:

1. Instructions: A task for the model to do. (Task description or instruction on how the model should perform)

2. Context: External information to guide the model.

3. Input data: The input you want a response for.

4. Output indicator: The output type or format.

Prompts don't require all four elements. Their structure depends on the task. You'll go through some examples soon.



![abstract-text](https://static.us-east-1.prod.workshops.aws/public/7595005b-ec55-488b-8126-d53d901877d1/static/050/050-prompt-overview.jpg)

With experimentation, you'll gain intuition for crafting and optimizing prompts to best suit your needs and models. Prompt engineering is an iterative skill that improves with practice.

[Prompt Engineering Patterns](#prompt-engineering-patterns)

## Prompt Engineering Patterns

[Zero-Shot](#zero-shot)

### Zero-Shot

Zero Shot prompting describes the technique where you present a task to an LLM without giving it further examples. You, therefore, expect it to perform the task without getting a prior look.

Modern LLMs demonstrate remarkable zero-shot performance, and a positive correlation can be drawn between model size and zero-shot performance.
Here is an example of a prompt , use it in the playground with Anthropic Claude model

```python
Human: 
Sulfuric acid reacts with sodium chloride, and gives <chemical1>_____</chemical1> and <chemical2>_____</chemical2>:
Assistant: the chemical1 and chemical 2 are:
```

Example executed on Amazon Bedrock text playground:

![zero-shot](https://static.us-east-1.prod.workshops.aws/public/7595005b-ec55-488b-8126-d53d901877d1/static/050/050-claude-zero-shot.png)

[Few-Shot](#few-shot)

### Few-Shot

Giving the model more information about the tasks at hand via examples is called Few-Shot Prompting. It can be used for in-context learning by providing examples of the task and the desired output. You can therefore condition the model on the examples to follow the task guidance more closely.

Here is an example of a prompt , use it in the playground with e Amazon Titan model

```python
Tweet: "I hate it when my phone battery dies.”: Sentiment: Negative
Tweet: "My day has been great”: Sentiment: Positive
Tweet: "This is the link to the article”: Sentiment: Neutral
Tweet: "This new music video was incredible” Sentiment:
```


Example executed in the Amazon Bedrock text playground:

![zero-shot](https://static.us-east-1.prod.workshops.aws/public/7595005b-ec55-488b-8126-d53d901877d1/static/050/050-titan-few-shot.png)

[Chain-of-Thought (with Few-Shot)](#chain-of-thought-(with-few-shot))

### Chain-of-Thought (with Few-Shot)

Chain-of-Thought (CoT) prompting breaks down complex reasoning tasks through intermediary reasoning steps. Chain-of-Thought prompts are usually very specific to a problem type. One can try to invoke CoT reasoning by using the trigger phrase "(Think Step-by-Step)". Let's examine the following example of a few-shot CoT prompt.

Here is an example of a prompt , use it in the playground with e Amazon Titan model

```python
On a given week, the viewers for a TV channel were
Monday: 6500 viewers
Tuesday: 6400 viewers
Wednesday: 6300 viewers


Question: How many viewers can we expect on Friday?
Answer: Based on the numbers given and without any more information, there is a daily decrease of 100 viewers. If we assume this trend will continue during the following days, we can expect 6200 viewers on the next day that would be Thursday, and therefore 6100 viewers on the next day that would be Friday.


Question: How many viewers can we expect on Saturday? (Think Step-by-Step)
Answer:
```

Hint: You can test following prompt in Amazon Bedrock text playground with distinct models

Run it with the Anthropic Claude model and check if the results are ok

