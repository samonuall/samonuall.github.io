---
layout: post
title: Fine-Tuning LLMs for System Initiative Prediction 
imagepath: /public/research_poster.png
subtitle: Group project in an undergraduate research program completed during winter break of my junior year. I was the main contributor to our code which fine-tuned Llama-7b on MSDialog data.
---

# Background #
A Conversational Information Seeking system (CIS systems): is “a task-oriented sequence of exchanges between ≥1 users and an information system…\[encompassing\] user goals that include complex information seeking and exploratory information gathering, including multi-step task completion and recommendation.” [\[1\]](https://sigir.org/wp-content/uploads/2018/07/p034.pdf)

The difference between CIS and a Google search is that a CIS system seemingly “understands” your question, and acts accordingly, whether that be asking a clarifying question, requesting more information, or just answering the original question. This process of the CIS system deciding whether to directly answer the question or get more information is called system initiative prediction. 

**Research Question: Does aligning a large language model (LLM) with supervised fine-tuning help its performance on the system initiative prediction task?**

# Dataset #
The MSDialog dataset is a labeled dialog dataset of question answering (QA) interactions between information seekers and answer providers from an online forum on Microsoft products [[2]](https://ciir.cs.umass.edu/downloads/msdialog/). We specifically use the MSDialog-Intent dataset prepared by the UMass CIIR lab, in which each conversation is broken down into labeled "utterances." An utterance is labeled using one of the 12 labels, 7 of which are system initiative tags which we are interested in predicting. Example system initiative labels are "Original Question" and "Clarifying Question." 


# Conclusion #
The fine tuned model performed badly overall, mainly due to its tendency to over-predict system initiative. However, it had high precision in cases where no initiative was needed with an accuracy of 76.7%. The few shot model was more of the same, however the accuracy of negative labels is better than the fine tuned model (88%), and worse on the positive labels. This is most likely because training was done without a weighted loss, and because no classification head was used. The training set was made up of 72% negative labels, which also may explain the model’s better performance for these situations. 

# Areas of Future Improvement #
Use a text-classification head on the LLM. Due to time constraints of the project, we had to settle on finetuning the model on data and getting its predictions from text output. Having a model made specifically made for classification training would have probably resulted in better performance. Weighted loss to compensate for large majority of negative samples would also most likely improve performance, but due to time constraints we did not have time to implement this.



# Slides and Code #
[Link to poster](https://docs.google.com/presentation/d/1muwB6UU91n_QL6_V17CcpIHUlaqSMgGLtmEcs9U0Fcg/edit?usp=sharing)
\\
[Code](https://colab.research.google.com/drive/1Jud-_r0wpBRpk6IyCk5PfVVZCgFxPi3Z?usp=sharing)