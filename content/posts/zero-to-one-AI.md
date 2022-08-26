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

* Just as the "unicorn" startup in a VC fund is more valuable than all others in the fund combined, **AI plugged into the "unicorn" use-case creates more value than all other use-cases combined**. 

The salient question becomes: What is the most promising opportunity for AI integration given the commercial context? 

In this blog post, I argue that applying “technology startup fundamentals” to AI development helps your team attend to that question early on and often throughout a project. While no silver bullet, this methodology lets you frame AI innovation projects as a business plan, with the hope of finding the strongest opportunities for value creation. This lets you avoid “bad luck” during development (and, usually, helps you win buy-in from executives).

<br><br>
## A primer on AI 
---
<br><br>
First, what’s AI and machine learning anyways? While you’ve probably heard of Artificial Intelligence, let’s clearly define its practical meaning in digital transformation. AI refers to computer programs that automate predictive tasks. In other words, they’re automatic data labelers. Some common examples include: What’s the sentiment of a tweet? What’s contained in an image? What’s the meaning of a phrase in a different language? For such tasks, there often isn’t a set of pre-defined rules a computer program can use to make good predictions. Instead, most of today’s AI tools rely on machine learning (ML) models for prediction. 

Machine learning models make predictions based on patterns in historical data. Certain patterns become surfaced because they were more correlated to the outcome (in the observations used for model training). Google’s Cassie Kozykrov likens training a machine learning model to a chef learning a recipe. This is a great analogy: in the case of a Twitter sentiment model, the model is following a recipe that it “learned” about positivity versus negativity in tweets, one that is based on the factors that drove sentiment in the historical tweets at hand. TL;DR: it’s following a recipe.

An ML model is really only capable of making sound predictions on new data when things closely resemble the dataset it was trained on. This "generalization problem" is one of the most impactful, pervasive, and talked about constraints of AI and machine learning today. The ramifications: the importance of training data for AI/ML cannot be exaggerated. You need great datasets to develop AI tools. In our tooling-enabled world, everyone mostly has access to the same types of models. Common ones include XGBoost, a tree-based architecture for tabular data, and Transformers, a Neural Net architecture for natural language and computer vision. Both of these models are used by practically every player in enterprise data science.

So, model algorithms don’t differentiate integrators of AI/ML. The leaders of AI integration are rather differentiated by their datasets (quality, scope, signal, commercial value, governance, importance/relevance to important business functions, etc.). The old adage “more data beats better models, but better data beats more data” is a core tenant of AI and machine learning. For example, if you wanted to develop an AI/ML tool that predicts customer health dynamics (like churn), you’d first need to invest in the data stack that can collect such customer data to train models on in the first place (see “Timing Question” below).  

With the basics under our belt, let’s dive into how startup fundamentals can help inform AI strategy.

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
 
Executives will be far more excited about investing in your AI/ML integration if you can make breakthrough progress on important problems to the business.  

In terms of the Engineering Question, developing AI/ML tools is no different from developing other types of technology: it needs to be significantly better in a key dimension than anything else available. If a simpler, more trusted, and less resource-intensive solution already exists for the problem, don’t go down the AI/ML route. AI tools in a lot of ways should be viewed as a last case scenario. Know when to take out the big AI/ML guns and when other solutions would suffice.  

The 10x magnitude improvement of the Engineering Question is in terms of value creation, not model accuracy, statistical significance, or some other technical metric. You’re AI/ML tool in commercial settings is not a research project or a modeling competition. What you’re looking for is whether or not an AI/ML tool creates significant improvement (10x or more) as a plug-in within the workstream. Yes, your model needs to meet a threshold for performance given the domain. In a greenfield space of machine learning, it’s possible your technology is significantly better than any other models out there. However, a model that’s on par with other solutions can be just as valuable when plugged into a workstream that otherwise doesn’t leverage the “magic sauce” value that the AI/ML tool enables. 

For example, in an NLP Accelerator project I undertook last summer, we developed two MVP prototypes that were powered by AI/ML tools (Transformer models, specifically). The Engineering Question were vastly different between the two. One tool had the potential to yield “more proprietary” machine learning because we were positioned to develop models that were more accurate than any open-source solution. The second tool had the smaller potential for making models proprietary, and where we could make models proprietary, they certainly were not anywhere near a 10x improvement on open-source options. However, the second model indeed delivered over 10x value when plugged into the workstream it was developed for. These engagements benefited greatly by AI integration because it enabled the use of alternative data in a completely new way – one that gelled well with the existing offerings and consistently delivered new insights therein for every deal of this type. In contrast, the second tool does not deliver a significant improvement when plugged into the workstream that it was designed for. And, while this wasn’t too concerning (we were aiming to flesh out the code paradigms to repeat this type of model for a new problem, and were less concerned about productizing) it meant that the tool was not a 10x improvement in a value creation lens – which is the key aspect when considering whether or not your AI/ML tool is a 10x improvement in commercial settings. 

**2 - The Timing Question**

“*Is now the right time to start your particular business?*”

“*Entering a slow-moving market can be a good strategy, but only if you have a definite and realistic plan to take it over.*”

Infrastructure readiness, social norms, government regulations, established platforms and ecosystems all play a role in the timing question.

Timing with infrastructure readiness re above

In the case of an internal tool, it may not matter whether or not you’re entering an existing market. Perhaps there is a strong value proposition in serving the tool internally with no external subscription cost. The timing question here more depends on whether people internally are ready to use the solution (in the case of a human-centered tool) or whether or not users would benefit from the modeling predictions (in the case of an automation tool). 

For an AI/ML tool that augments an existing offering, the Timing Question revolves less around the AI/ML solution itself and more around the offering it’s attaching to. Imagine you’re a consulting firm that sells a lot of engagements of “Workstream A”. Here, the Timing Question of adding AI/ML components to Workstream A depends on whether consultants working on these engagements are ready to add a new feature. Is there buy-in from the folks who are using the tool in the wild? 

The relevant factors of the Timing Question for AI/ML products that are subscription-based is most similar to the factors of a technology startup. This is in no small part because many technology companies are SaaS, which is essentially what a subscription AI tool is as well. Here, the saturation of the market, speed at which it’s moving, 

For example, take LinkedIn’s recommendation system. This AI/ML tool is an internal tool. The underlying solution may or may not be all that unique from other technology companies’ tools – but it doesn’t matter that recommendation systems tools are widely adopted across commercial markets (i.e., it’s similar to an existing market in some senses). What matters is that LinkedIn users wanted to use the tool – and that the users were ready for it. If users weren’t ready, then the product would have flopped. The timing question here also depends on how cheap external solutions would be – and whether or not they plug into your workstream in the right way. While a great, affordable AI/ML tool for your given domain may exist externally - if it doesn’t plug into your use-case in the best possible way, then perhaps developing an internal tool (that does fit in the best way) still makes sense to do. 


**3 - The Monopoly Question**

“*Are you starting with a big share of a small market?*”

“*A true innovation is one that has no competition. Exaggerating your own uniqueness is an easy way to botch the monopoly question.*"

“*Trillion-dollar markets mean ruthless, bloody competition*”

“*Customers won’t care about any particular technology unless it solves a particular problem in a superior way.*”

“*If you can’t monopolize a unique solution for a small market, you’ll be stuck with vicious competition.*”

“*Exaggerating your own uniqueness is an easy way to botch the monopoly question.*”

“*You can’t dominate a submarket if it’s fictional, and huge markets are highly competitive, not highly attainable.*” 

The monopoly question is critical when productizing subscription services. This is why I believe that developing AI/ML as internal tools or augmentation tools is easier than subscription services, and it comes down to how much you need to worry about the Monopoly Question. 

In the case of internal tooling, it’s fine if your solution is not monopolizing in nature, so long as it’s more effective or cheaper than other options. Ditto in the case of offering augmentation, your solution is already attached to existing business (an offering which ideally is itself a monopoly). In these cases, the goal is to monopolize the application of AI/ML in your business workstream, not necessarily develop AI/ML tools that have “monopoly potential”.

Consider Google’s DocumentAI offering. Unfortunately, this product doesn’t quite answer the monopoly question as well as Google Search does. One of the tool’s fundamental features is legal entity extraction from contracts. 1. Research paper that enables more teams to build. If it was an internal tool. If it was an augmentation. 

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
