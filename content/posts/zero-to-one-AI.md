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

In his book Zero to One, Peter Thiel explores the core fundamentals that successful technology startups have in common. The takeaway: startups should exude seven pivotal traits – otherwise, queue red flags. Here's why great AI innovation projects also exhibit the business fundamentals of successful technology startups, from the perspective of a Bay Area data scientist working in digital strategy consulting.  

<br><br>

<p align="center"> <img src="/posts/blog_AI_image_3.jpg"/ width = "500" height = "260"> </p>

<p align="center">
<body align="center">Photo by <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/@urielsc26">Uriel SC</a> on <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/photos/11KDtiUWRq4">Unsplash</a> </body>
</p>

<br><br>

This post will explore the similarities (and some of the differences) between technology startups and digital transformation, with a focus on applied AI. The intended audience includes data practitioners (DS, DE, etc.), technologists, and business executives - as both technical and non-technical folks closely touch AI integration. 

**TL;DR: Your applied AI project should adequately answer seven questions about its commercial viability, just like technology startups.** 

<br><br>
## Introduction
---
<br><br>

The parallels between technology startups and digital transformation are numerous. In both, the overarching goal is to create value through new applications of technology. And, today, integrating AI tools is more frequently a component of digital transformation (and, as it turns out, startups). According to Silvio Palumbo of BCG Gamma, companies of all shapes and sizes are posed to find a "competitive advantage" through the “Smart Integration” of AI tools today [1]. And, while this trend is largely enabled by improvements in the open-source and subscription-tools landscape, the commercial viability of AI innovation continues to hinge on value creation fundamentals.

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
* Note, all italicized quotes come from Chapter 13 of Peter Thiel’s book Zero to One [2]

---

<br><br>

**1 - The People Question**

“*Do you have the right team?*”

Assembling an effective applied AI team takes **the right mindset**. While engineering chops are certainly necessary to develop smart AI tools, it’s equally important to ensure that the team can **easily communicate results to business stakeholders, in the terms that executives care about** [3]. 

First, assign an empowered stakeholder, or project manager, that is closely connected with senior leadership. In a small company, perhaps this project manager is in fact a part of senior leadership. This stakeholder’s job is to act as the anchor for the innovation team, ensuring that development doesn’t stray from business lanes. Second, assemble a diversity of talents within a data science team. This way, ideas can cross-pollinate and tasks are executed by the best hands for the given job. More likely than not, your best communicator, designer, data scientist, and data engineer aren’t one person. In addition to the cross-pollination of talents and ideas, ensure that the team is seamlessly collaborating across workstreams. The more eyes and voices that can be heard at every step, technical or non-technical, the better. Applied AI innovation is not rocket science, but it’s also not a one-person job. Collaboration is key, no “hand-offs between groups” culture. Perhaps this level of real collaboration is easiest when working in the same physical room, but maybe not (remote work can be effective too, in my opinion). Either way, lead with a teamwork strategy even if talents are spread across different groups. 

“*Real technologists wear T-shirts and jeans [not suits]*”

Just as in technology startups, be wary of data science teams that don’t fit the “tech vibe”. This trend holds even in a more traditionally formal industry such as management consulting. Guaranteed that any data science group within a consulting firm presents differently than the business analysts (particularly if the group is in tech hubs, such as the Bay Area or Seattle). Walk into a firm's San Francisco office and chat with the data science team, odds are that these folks will remind you of technologists much more than business analysts in the New York City or Chicago offices will. If they don’t, hire a different strategy consulting firm for digital transformation. 

<br><br>

**2 - The Distribution Question**

“*Do you have a way to not just create but deliver your product?*”

But, it’s not just enough to gather an effective array of talent. Your team needs to execute a tried and trusted plan. Here's how Cassie Kozyrkov, Google's Chief Decisions Officer, ensures that applied AI projects consider delivery throughout their lifecycle [4]. Firstly, at the beginning of a project, make sure you “reality check” and “define your objectives”. While it’s a little weird to think about delivery at the beginning of a project, not doing so is perhaps the easiest way to create solutions with no real commercial value and/or deployment viability. Imagine that the system is in production and outputs are being generated. How are people benefiting from the predictions? What’s the value proposition of integrating the tool at scale? 

You’ll also want to ask yourself reality-check questions: like whether or not simpler solutions worked, if there’s data available to learn from, how you will deploy at a systems level, if you have the compute hardware, and so on. When defining objectives at the start of development, consider the operational system in the product once again. What objectives need to be met to reach project success for the product? Make sure to clearly define objectives **in business terms, the ones that executives will listen carefully to**. 

“*Selling and delivering a product is at least as important as the product itself.*”

After the ideation phase of a product (one that was ideally based on sound business objectives and passed the reality checks), you’re ready to start considering product deployment. For AI/ML, deploying models into production is their delivery, well, along with other considerations in many cases (the user interface, analytics wrappers, visualization wrappers, real-time active learning, “human-in-the-loop” decision-making, monitoring, unit testing, etc.). Carly Taylor of Activision ML advises practitioners to consider the following questions for deployment: “When? How often? Where? What do you do with the predictions? … you’re building something that will be used for real. What is our [systems-level deployment] policy for what we build?”. [5] Answering these questions even at the beginning of a project, when setting objectives, is a great way to focus on the delivery of the product, which is how models actually create value in the first place. 

<br><br>

**3 - The Engineering Question**

“*Companies must strive for 10x better because merely incremental improvements often end up meaning no improvement at all for the end user.*"

It’s up to you and your innovation team to find opportunities to create breakthrough technology, technology that help customers with their real problems in a substantial way. Make sure AI/ML tooling can seriously deliver value to the end-user. In the words of Cassie Kozyrkov, applied AI tools are “not for one-offs” [x] – they should deliver value to important, frequent workstreams that need “an impressive number of items labeled”. 

“*Only when your product is 10x better can you offer the customer transparent superiority.*”
 
Executives will be far more excited about investing in your AI/ML integration if you create technology with 10x innovation potential – just like VC investors in technology. 

<br><br>

**4 - The Secret Question**

“*Have you identified a unique opportunity that others don't see?*”

Model algorithms don’t usually differentiate leaders of AI/ML integration. Secrets in AI integration are more frequently differentiated by 1. datasets and by 2. use-case attach points - this is where to focus your search for “unique opportunities that others don't see”. 

1. **Datasets** that are high quality have an adequate scope, signal, governance, and relevance to important business workstreams. The old adage **“more data beats better models, but better data beats more data” is a core tenant of enterprise AI**. For example, if you wanted to develop an AI/ML tool that predicts customer health dynamics (like churn), you’d first need to invest in the data stack that stores customer event data in a comprehensive way. When first modernizing data capture in a business, it makes sense to first turn to data analytics over AI/ML. For example, first develop analytics solutions such as metrics tracking and churn cohort analysis, before adding in AI tooling to the picture. And, as discussed in question 2, perhaps non-AI solutions can work adequately for the use-case. Take churn prediction for example. First, ask yourself (by digging into the data), are there trends in cohort analysis, such as power usage, that correlate to churn? Perhaps this simple rule can adequately forecast churn in the future for the given situation. Or, perhaps focusing on other leading indicators of churn, such as customer complaints, helps you adequately gain an initial POV on future churn. Either way, ensure the “unique opportunity” is right for AI and differentiated from competitors through its “secrets” (i.e., through the use of high-quality proprietary datasets). 

2. **Use-case attach points** of AI often already have a “secret sauce” to them. Say you’re in the financial services industry and one of your company’s offerings already is differentiated in the market – it has good traction, and you do lots of these kinds of engagements. See if AI/ML can deliver greenfield value to widen your marketplace lead by expanding your most important business. In short, search for use-case attach points where models plug in well commercially. You don’t even necessarily need proprietary datasets to do this well, depending on the situation, you can still **reap outsized returns from AI integration when the use-case attach point has that “secret sauce” (regardless of how proprietary the underlying models are)**. 

“*Great companies have secrets: specific reasons for success that other people don’t see.*”

<br><br>

**5 - The Timing Question**

“*Is now the right time to start your particular business?*”

“*Entering a slow-moving market can be a good strategy, but only if you have a definite and realistic plan to take it over.*”

Infrastructure readiness, social norms, government regulations, established platforms and ecosystems all play a role in the timing question.

* AI pyramid -> DE lecture slide

<br><br>

**6 - The Monopoly Question**

“*Are you starting with a big share of a small market?*”

“*Monopoly is the condition of every successful business.*”

“*A true innovation is one that has no competition. Exaggerating your own uniqueness is an easy way to botch the monopoly question.*"

“*Trillion-dollar markets mean ruthless, bloody competition*”

“*Customers won’t care about any particular technology unless it solves a particular problem in a superior way.*”

“*If you can’t monopolize a unique solution for a small market, you’ll be stuck with vicious competition.*”

“*Exaggerating your own uniqueness is an easy way to botch the monopoly question.*”

“*You can’t dominate a submarket if it’s fictional, and huge markets are highly competitive, not highly attainable.*” 

<br><br>

<p align="center"> <img src="/posts/monopoly.jpg"/ width = "500" height = "300"> </p>

<p align="center">
<body align="center">Photo by <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/@rwlinder">Robert Linder</a> on <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/photos/xDgwGGBuPdc">Unsplash</a> </body>
</p>

<br><br>


**7 - The Durability Question**

“*Will your market position be defensible 10 and 20 years into the future?*”

“*Every entrepreneur should plan to be the last mover in her particular market.*”

“*What will the world look like 10 to 20 years from now, and how will my business fit in?*”

“*What will stop [x] from wiping out my business?*”



<br><br>
## Conclusion 
---
<br><br>

Conclude and link to relevant articles


<br><br>
## Appendix: AI/ML Background 
---
<br><br>

Today’s state-of-the-art machine learning models make predictions based on patterns in historical data. These patterns correspond to correlations between model features (the dataset) and the outcome (the label prediction) and are specific to the training dataset employed. Google’s Cassie Kozykrov likens training a machine learning model to a chef learning a recipe. This is a great analogy: in the case of a Twitter sentiment model, the model is following a recipe that it “learned” about positivity versus negativity in tweets, one that is based on the factors that drove sentiment in the historical tweets at hand. TL;DR: it’s following a recipe.

An ML model is really only capable of making sound predictions on new data when things closely resemble the dataset it was trained on. This "generalization problem" is one of the most impactful, pervasive, and talked about constraints of AI and machine learning today. The ramifications: the importance of training datasets cannot be exaggerated. You need great datasets to develop AI tools. In our tooling-enabled world, everyone mostly has access to the same types of models. Common ones include XGBoost, a tree-based architecture for tabular data, and Transformers, a Neural Net architecture for natural language and computer vision. Both of these models are used by practically every player in enterprise data science. Interestingly, most of the state-of-the-art, truly massive models developed by the Microsofts of the world (the ones that are on the top of benchmark leaderboards such as <a target="_blank" rel="noopener noreferrer" href="https://super.gluebenchmark.com/">SuperGLUE</a> for natural language processing) are **not** efficient enough in terms of latency to deploy in most commercial settings. So, even though these proprietary models may appear superior if you glance at benchmark leaderboards, they aren’t efficient enough to scale in the wild. 

Model algorithms don’t differentiate integrators of AI/ML. The leaders of AI integration are rather differentiated by their datasets (quality, scope, signal, commercial value, governance, importance/relevance to important business functions, etc.). The old adage “more data beats better models, but better data beats more data” is a core tenant of enterprise AI. For example, if you wanted to develop an AI/ML tool that predicts customer health dynamics (like churn), you’d first need to invest in the data stack that can collect such customer datasets specific to your business in the first place (see “Timing Question” above).  

<br><br>
## Citations
---
<br><br>


[1] S. Palumbo, <a target="_blank" rel="noopener noreferrer" href="https://medium.com/bcggamma/smart-integration-four-levels-of-ai-maturity-and-why-its-ok-to-be-at-level-3-2af0c94c9614">Smart Integration: Four levels of AI maturity, and why it’s OK to be at Level 3</a> (2022), Gamma – Part of BCG X
<br><br>
[2] T. Peter, M. Blake. Zero to one: notes on startups, or how to build the future (2014),  New York Crown Business (Printed Book)
<br><br>
[3] S. Berinato, <a target="_blank" rel="noopener noreferrer" href="https://hbr.org/2019/01/data-science-and-the-art-of-persuasion">Data Science and the Art of Persuasion: Organizations struggle to communicate the insights in all the information they’ve amassed. Here’s why, and how to fix it.</a>  (2019), Harvard Business Review
<br><br>
[4] C. Kozyrkov, <a target="_blank" rel="noopener noreferrer" href="https://medium.com/swlh/12-steps-to-applied-ai-2fdad7fdcdf3">12 Steps to Applied AI: A roadmap for every machine learning project</a> (2019), The Startup
<br><br>
[5] C. Taylor, D. Liu, <a target="_blank" rel="noopener noreferrer" href="https://www.youtube.com/watch?v=JkXgLyzqJg0">Using ML to tackle disruptive behaviors in gaming - Carly Taylor - the data scientist show 045</a> (2021), The Data Scientist Show
<br><br>
[6] M. Rogati, <a target="_blank" rel="noopener noreferrer" href="https://hackernoon.com/the-ai-hierarchy-of-needs-18f111fcc007">The AI Hierarchy of Needs</a> (2017), Hackernoon
