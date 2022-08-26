---
title: "Why startup fundamentals are key to AI strategy"
date: 2022-08-16
katex: true
markup: "mmark"
---


# Why startup fundamentals are key to AI strategy

## Using the “technology startup mentality” to integrate technology in commercial contexts
---

### Blog Post Currently Under Construction 

<br><br>

In his book Zero to One, Peter Thiel explores the core fundamentals that successful technology startups have in common. The takeaway: startups should exude seven pivotal traits – otherwise, queue red flags. Is AI strategy analogous to new technology ventures?

<br><br>

<p align="center"> <img src="/posts/blog_AI_image_2.jpeg"/ width = "475" height = "225"> </p>

<br><br>

This post will explore the similarities (and some of the differences) between technology startups and AI-powered digital transformation. The intended audience includes data practitioners (DS, DE, etc.), technologists, and business executives - as both technical and non-technical roles touch AI strategy. 

Here's why AI innovation teams should exude the mentality of a technology startup, from the perspective of a Bay Area data scientist in strategy consulting.  

<br><br>
## Introduction
---
<br><br>

The parallels between technology startups and digital transformation are numerous. In both, the overarching goal is to create value through new applications of technology. And, today, integrating AI tools is more frequently a component of digital transformation (and, as it turns out, technology startups). According to Silvio Palumbo of BCG Gamma, companies of all shapes and sizes are posed to find a "competitive advantage" through the “Smart Integration” of AI tools today (insert Silvio Palumbo citation). And, while this trend is largely enabled by improvements in the open-source and subscription-tools landscape, the commercial viability of AI innovation continues to hinge on value creation fundamentals.

> The "unicorn" startup in a VC fund is more valuable than all others (in the fund) combined.<br><br>
>  **Similarly, an AI tool plugged into the "unicorn" use-case creates more value than all other options combined**. 

The salient question becomes: What is the most promising opportunity for AI integration given the commercial context? 

In this blog post, I argue that applying “technology startup fundamentals” to AI development helps your team attend to that question early on and often throughout a project. While no silver bullet, this methodology lets you frame AI innovation projects as a business plan, with the hope of finding the strongest opportunities for value creation. This lets you avoid “bad luck” during development (and, usually, helps you win buy-in from executives).

<br><br>
## A primer on AI 
---
<br><br>
First, what’s AI and machine learning anyways? While you’ve probably heard of Artificial Intelligence, let’s clearly define its practical meaning in digital transformation. AI refers to computer programs that automate predictive tasks. In other words, they’re automatic data labelers. Some common examples include: What’s the sentiment of a tweet? What’s contained in an image? What’s the meaning of a phrase in a different language? For such tasks, there often is **not** a set of pre-defined rules a computer program can use to make good predictions (if-else/and-or rules are tenants of “traditional” computer programming). Instead, most of today’s AI tools rely on machine learning (ML) models for prediction, the brainchild of a different field from computer science, the field of statistical learning. 

For more background on AI/ML, see the appendix section.  
<br><br>
## Mapping startup fundamentals to AI strategy
<br>
* Note, all italicized quotes come from Chapter 13 of Peter Thiel’s book *Zero to One*. 

---

<br><br>

**1 - The Engineering Question**

“*Can you create breakthrough technology instead of incremental improvements?*”

“*Companies must strive for 10x better because merely incremental improvements often end up meaning no improvement at all for the end user.*"

“*Only when your product is 10x better can you offer the customer transparent superiority.*”
 
Executives will be far more excited about investing in your AI/ML integration if you can make breakthrough progress on important problems for the business.  


**2 - The Timing Question**

“*Is now the right time to start your particular business?*”

“*Entering a slow-moving market can be a good strategy, but only if you have a definite and realistic plan to take it over.*”

Infrastructure readiness, social norms, government regulations, established platforms and ecosystems all play a role in the timing question.


**3 - The Monopoly Question**

“*Are you starting with a big share of a small market?*”

“*A true innovation is one that has no competition. Exaggerating your own uniqueness is an easy way to botch the monopoly question.*"

“*Trillion-dollar markets mean ruthless, bloody competition*”

“*Customers won’t care about any particular technology unless it solves a particular problem in a superior way.*”

“*If you can’t monopolize a unique solution for a small market, you’ll be stuck with vicious competition.*”

“*Exaggerating your own uniqueness is an easy way to botch the monopoly question.*”

“*You can’t dominate a submarket if it’s fictional, and huge markets are highly competitive, not highly attainable.*” 

**4 - The People Question**

“*Do you have the right team?*”

“*Real technologists wear T-shirts and jeans [not suits]*”

“So much of innovation is about the quality of people and culture you have. And finding a technical advancement which is 10X better, means having engineers and technical people to do it.” 

Reference HBS article. 

It’s not just enough to gather a diverse array of data talent. You’re leaders and managers need to eat and breathe the right kind of execution framework – which enables your team to productize effectively. 

Ask the right questions, get the right data, train models on the data, evaluate models on new data, productize the solution, make sure launching is a good idea, keep production system reliable over time

**5 - The Distribution Question**

“*Do you have a way to not just create but deliver your product.*”

In the words of Dave McCLure of 500 Startups, “Customers don’t care about your solution. They care about their problems.” 

“*Selling and delivering a product is at least as important as the product itself.*”


When considering the timing question for any AI/ML product, consider the customer’s problem above all else. Will they have the same problems in two years? Are they ready for the solution you’re ideating? You’re AI/ML tool needs to deliver value now and in the future – after all – companies are evaluated based on potential future cash flow. 


“You might think your technology speaks for itself, but it most probably doesn’t. You still need an effective distribution channel. Primarily a way to get close to the customer, so they can experience the superior advantage you can bring.”

**6 - The Durability Question**

“*Will your market position be defensible 10 and 20 years into the future?*”

“*Every entrepreneur should plan to be the last mover in her particular market.*”

“*What will the world look like 10 to 20 years from now, and how will my business fit in?*”

“*What will stop [x] from wiping out my business?*”


**7 - The Secret Question**

“*Have you identified a unique opportunity that others don't see?*”

“*Great companies have secrets: specific reasons for success that other people don’t see.*”

<br><br>
## Appendix: AI/ML Background 
---
<br><br>

Today’s state-of-the-art machine learning models make predictions based on patterns in historical data. These patterns correspond to correlations between model features (the dataset) and the outcome (the label prediction) and are specific to the training dataset employed. Google’s Cassie Kozykrov likens training a machine learning model to a chef learning a recipe. This is a great analogy: in the case of a Twitter sentiment model, the model is following a recipe that it “learned” about positivity versus negativity in tweets, one that is based on the factors that drove sentiment in the historical tweets at hand. TL;DR: it’s following a recipe.

An ML model is really only capable of making sound predictions on new data when things closely resemble the dataset it was trained on. This "generalization problem" is one of the most impactful, pervasive, and talked about constraints of AI and machine learning today. The ramifications: the importance of training datasets cannot be exaggerated. You need great datasets to develop AI tools. In our tooling-enabled world, everyone mostly has access to the same types of models. Common ones include XGBoost, a tree-based architecture for tabular data, and Transformers, a Neural Net architecture for natural language and computer vision. Both of these models are used by practically every player in enterprise data science. Interestingly, most of the state-of-the-art, truly massive models developed by the Microsofts of the world (the ones that are on the top of benchmark leaderboards such as SUPERGLUE) are **not** efficient enough in terms of latency to deploy in most commercial settings. So, even though these proprietary models may appear superior if you glace at benchmark leaderboards, they aren’t efficient enough to scale in the wild. 

So, model algorithms don’t differentiate integrators of AI/ML. The leaders of AI integration are rather differentiated by their datasets (quality, scope, signal, commercial value, governance, importance/relevance to important business functions, etc.). The old adage “more data beats better models, but better data beats more data” is a core tenant of enterprise AI. For example, if you wanted to develop an AI/ML tool that predicts customer health dynamics (like churn), you’d first need to invest in the data stack that can collect such customer datasets specific to your business in the first place (see “Timing Question” above).  
![image](https://user-images.githubusercontent.com/67394384/186981127-6c5be8aa-9eae-4c42-becd-fe6b170141fc.png)
