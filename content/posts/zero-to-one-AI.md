---
title: "Why startup fundamentals are key to AI strategy."
date: 2022-08-16
katex: true
markup: "mmark"
---


# Why startup fundamentals are key to AI strategy

## Using the “technology startup mentality” to integrate technology in commercial contexts
---

[Published in Towards Data Science](https://towardsdatascience.com/why-startup-fundamentals-are-key-to-ai-strategy-76e5a59d9b96)
<br><br>

In his book Zero to One, Peter Thiel explores the core fundamentals that successful technology startups have in common. The takeaway: startups should embrace seven pivotal traits — otherwise, queue red flags. Here’s why great AI innovation projects also exhibit the fundamentals of successful technology startups, from the perspective of a Bay Area data scientist working in digital strategy consulting.

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

The parallels between technology startups and digital transformation are numerous: the overarching goal is to create value through novel applications of technology. According to Silvio Palumbo of BCG Gamma, companies of all shapes and sizes are posed to find a “competitive advantage” through the “Smart Integration” of AI tools in digital transformation today [1]. And, while this trend is largely enabled by improvements in the open-source and subscription-tools landscape, the commercial viability of AI innovation continues to hinge on value creation fundamentals, high-level strategy, and buy-in from executives.

> The "unicorn" startup in a VC fund is more valuable than all others (in the fund) combined.<br><br>
>  **Similarly, an AI tool plugged into the "unicorn" use-case creates more value than all other options combined**. 

The salient question becomes: What is the most promising opportunity for AI integration given the business context?

In this blog post, I argue that applying “technology startup fundamentals” to AI development helps your team attend to that question early and often throughout a project. While no silver bullet, this methodology lets you frame AI innovation projects as a business plan, with the goal of finding the strongest opportunity for value creation. And, ultimately, it lets you avoid “bad luck” during development (and, usually, helps win buy-in from executives).

<br><br>
## A primer on AI 
---
<br><br>
First, what are AI and machine learning? While you’ve probably heard of Artificial Intelligence, let’s clearly define its practical meaning in digital transformation. AI refers to computer programs that automate predictive tasks. In other words, they’re automatic data labelers. Some common examples include: What’s the sentiment of a tweet? What’s contained in an image? What’s the meaning of a phrase in a different language? For such tasks, there often is not a set of pre-defined rules a computer program can use to make good predictions (if-else/and-or rules are tenants of “traditional” computer programming). Instead, most of today’s AI tools rely on machine learning (ML) models for prediction, the brainchild of a different field from computer science, the field of statistical learning.

For more background on AI/ML, see the appendix section.
<br><br>
## Mapping startup fundamentals to AI strategy
<br>
* Note, all italicized quotes come from Chapter 13 of Peter Thiel’s book Zero to One [2].

---

<br><br>

**1 - The People Question**

“*Do you have the right team?*”

While engineering chops are necessary to develop smart AI tools, it’s equally important to ensure that your data science team can communicate results effectively to business stakeholders [3]. Use the right mindset to assemble an effective team.

First, assign an empowered stakeholder as the project manager, a person that is closely connected with senior leadership. Their job is to act as the bridge between the innovation team and executives, ensuring that development doesn’t stray from prescribed business lanes.

Tech sage Paul Graham emphasizes that companies must empower their best developers. Do so in a way that matches talents to roles by assembling a diverse array of talents. This way, ideas cross-pollinate and development tasks are executed by the best available hands. Your top communicator, deck designer, machine learning engineer, software developer, and data engineer aren’t one person. Applied AI innovation is not a one-person job. Collaboration is key (there shouldn’t be any hand-offs between groups).

“*Real technologists wear T-shirts and jeans [not suits]*”

<br><br>

**2 - The Distribution Question**

“*Do you have a way to not just create but deliver your product?*”

It’s not just enough to gather the right array of talent. Your team needs to execute a tried and trusted plan. Here’s how Cassie Kozyrkov, Google’s Chief Decisions Officer, ensures that applied AI projects consider delivery throughout their lifecycle [4]. Firstly, at the beginning of a project, make sure you “reality check” and “define your objectives”. Not doing so is perhaps the easiest way to create solutions with no real commercial value. Imagine that the system is in production and outputs are being generated. How are people benefiting from the predictions? What’s the value proposition of integrating the tool at scale?

You’ll also want to ask yourself reality-check questions: like whether or not simpler solutions worked, if there’s data available to learn from, how you will deploy at a systems level, if you have the budget for project costs, and so on.

When defining objectives at the start of development, consider the operational product again. What objectives need to be met to reach project success? Make sure to clearly define objectives in the business terms that executives will listen to carefully.

“*Selling and delivering a product is at least as important as the product itself.*”

Delivery for AI/ML comes down to the deployment of models in production, which make predictions at the scale of your entire business. In most cases, there are many factors to deployment beyond the actual predictions (the user interface, analytics wrappers, visualization wrappers, real-time active learning, “human-in-the-loop” decision-making, monitoring, unit testing, latency requirements, hardware requirements, systems requirements, etc.). Carly Taylor of Activision ML advises data practitioners to consider the following questions for predicting in the wild: “When? How often? Where? What do you do with the predictions? … You’re building something that will be used for real. What is our [systems-level] policy for what we build?” [5]. Attending to these questions before, during, and after development helps projects effectively create value in the first place.

<br><br>

**3 - The Engineering Question**

“*Companies must strive for 10x better because merely incremental improvements often end up meaning no improvement at all for the end user.*"

It’s up to you and your innovation team to find opportunities for breakthrough technology. Make sure AI/ML tooling can seriously deliver value to the end-user. In the words of Cassie Kozyrkov, applied AI tools are “not for one-offs”– they should deliver value to important, frequent workstreams that need “an impressive number of items labeled” [4].

“*Only when your product is 10x better can you offer the customer transparent superiority.*”
 
Executives will be far more excited about investing in your AI/ML project if you create technology with 10x innovation potential — just like Silicon Valley VC investors and technology startups.

<br><br>

**4 - The Secret Question**

“*Have you identified a unique opportunity that others don't see?*”

Model algorithms aren’t usually the secrets that differentiate leaders of AI/ML integration. Secrets in AI are more frequently 1. datasets and/or 2. use-cases — this is where to focus your search for “unique opportunities that others don’t see”.

1.	Datasets of high quality have adequate scope, signal, governance practices, and relevance to important business workstreams. The old adage “more data beats better models, but better data beats more data” is a core tenant of enterprise AI. For example, if you wanted to develop an AI/ML tool that predicts customer health dynamics (like churn), you’d first need to invest in the data stack that stores customer event data in a comprehensive way (see more below in the “Timing Question”). And, as discussed in the “Distribution Question”, perhaps non-AI solutions can work adequately for the given use-case. Take churn prediction again. First, ask yourself (by digging into the data): Are there trends in your cohort analysis, such as power usage, that correlate to churn? Perhaps this simple rule can adequately forecast churn in the future for the given situation. Or, perhaps focus on other leading indicators of churn, such as customer complaints, to help you gain an initial POV on the future. Either way, ensure the “unique opportunity” is right for AI and differentiated from competitors.
2.	The best use-case, in your venture, for applied AI often already has a “secret sauce” on its own. Say you’re in the financial services industry and one of your offerings is differentiated in the market — you perform these engagements regularly. See if AI/ML can deliver greenfield value to widen your marketplace lead, in the process expanding your most important business. Search for use-cases where models plug in well. This way, you don’t necessarily need proprietary datasets to create valuable AI tooling. You can still reap outsized returns from AI integration when models create value for use-cases that have that “secret sauce” (regardless of how proprietary the underlying models are).

“*Great companies have secrets: specific reasons for success that other people don’t see.*”

<br><br>

**5 - The Timing Question**

“*Is now the right time to start your particular business?*”

Monica Rogati’s blog on Hackernoon, “The AI Hierarchy of Needs”, is perhaps the most well-known piece on AI timing [6]. It’s been read nearly 200,000 times. AI and deep learning are positioned at the very tip of the “hierarchy of needs” pyramid. For AI innovation teams, it’s helpful to think of your deep learning models as the tip of an iceberg, sitting on top of a large mass of data engineering, data governance, infrastructure, and data analytics. At the very start of a company’s dip into data-native, it often makes sense to turn to analytics before AI/ML. For example, say you’re a SaaS business interested in churn analysis. Before adding AI tooling, develop analytics solutions such as metrics tracking and cohort analysis to mine insights in a leaner way. Know when your AI integration project is premature. Near the end of the article, Rogati touches on how you can bring the “Minimum Viable Product” (MVP) ethos to applied AI, while still respecting your timing and readiness.

> “The data science hierarchy of needs is not an excuse to build disconnected, over-engineered infrastructure for a year. Just like when building a traditional MVP (minimally viable product), you **start with a small, vertical section of your product and you make it work well end-to-end. You can build its pyramid, then grow it horizontally.** … We did not build an all-encompassing infrastructure without ever putting it to work end-to-end.” [6].

And, consider AI/ML solutions that take a smaller amount of resources to get started for MVP development with tight resources or low executive buy-in, — for example, where open-source datasets can be used (think things like sentiment analysis). To convince stakeholders, it’s sometimes useful to pitch the project with an MVP in your back pocket. Consider creating a baseline model and deploying it in a sandbox (so that stakeholders can see its potential at their fingertips).

If you’re an executive, talk to your technical people about blogs like Rogati’s. Consider your appetite for investment in tools and relevant timing concerns in the world at large (governmental policy changes, privacy regulations, customer feedback, market saturation, etc.).

<br><br>

**6 - The Monopoly Question**

“*Monopoly is the condition of every successful business.*”

“*You can’t dominate a submarket if it’s fictional, and huge markets are highly competitive, not highly attainable. … Exaggerating your own uniqueness is an easy way to botch the monopoly question.*”

<br><br>

<p align="center"> <img src="/posts/monopoly.jpg"/ width = "500" height = "300"> </p>

<p align="center">
<body align="center">Photo by <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/@rwlinder">Robert Linder</a> on <a target="_blank" rel="noopener noreferrer" href="https://unsplash.com/photos/xDgwGGBuPdc">Unsplash</a> </body>
</p>

The first thought that comes to mind on (real business) monopolies for me: <a target="_blank" rel="noopener noreferrer" href="https://www.google.com/">Google Search</a>. “Google” serves as the de-facto verb for searching information online. If you look up Search’s worldwide market share for all search engines (by Googling it) you’ll see that it’s over 90%. It’s a definitive monopoly in an entire marketplace. And, if you’re Google, it makes perfect sense to integrate AI/ML tools within Search. Let’s focus on one thread (among a massive list) of applied AI integrations within Search today: BERT. In 2017, Google researchers published “Attention Is All You Need”, which introduced the Transformer architecture of neural network models. Fast forward to 2019, and a Google blog post asserts that the integration of BERT models, a natural language iteration of the Transformer model, resulted in “the biggest leap forward in the past five years, and one of the biggest leaps forward in the history of Search” [7]. The lesson to learn? Attach great AI/ML tools within the strongest part of your business.

Now, let’s look at another Google product: <a target="_blank" rel="noopener noreferrer" href="https://cloud.google.com/solutions/contract-doc-ai">Contract DocAI </a>. This digital AI/ML tool enables subscribers to better understand their contracts. Features include legal entity extraction (surfacing important contract information) and Optical Character Recognition. In fact, Gartner crowned Google the market leader in the “Forrester Wave: Document-Oriented Text Analytics Platforms, Q2 2022”. Consider whether you think Google Contract DocAI is a monopoly?

Let’s first ask ourselves what the entire market is for this SaaS technology. Is it Forrester’s identified “Document-Oriented Text Analytics Platforms”? Amazon and Microsoft are both direct competitors with very similar solutions. Is it any and all software tools for contract files? It turns out that there are massive sister industries for Contracts AI, such as Contract Lifecycle Management (see the DocuSign CLM, for example). Is it any and all NLP tools in the field of applied AI? All AI/ML tooling? As you see, it’s tougher to define the global marketplace for this product. Monopolies are easiest to create when the entire marketplace isn’t already massive (and, ideally, has the potential to grow). Remember, “*Exaggerating your own uniqueness is an easy way to botch the monopoly question.*” 

<br><br>

**7 - The Durability Question**

“*Will your market position be defensible 10 and 20 years into the future?*”

“*What will stop [x] from wiping out my business?*”

The seventh and final startup fundamental is the “Durability Question”. The “outsized returns” on your AI integration are tied to their ability to deliver value in the future. After all, companies are valued on their future cash flows. In the field of applied AI, tooling moves rapidly. There’s no way to ensure any one solution will “be defensible 10 and 20 years into the future” in a field where the boundaries of state-of-the-art seem to expand every few months. It’s more important to phrase the “Durability Question” in terms of your AI strategy itself. Following a sound high-level strategy on value creation fundamentals and strong business planning, in the long run, ensures the durability of your AI/ML integration venture. And, as the “People Question” indicates, you’ll need the right in-house team of data scientists, or the right data science consultants contracted, to successfully pull off applied AI integration. The quality of your data science team is in it of itself a factor of the “Durability Question” and how differentiated your products are in the marketplace.

<br><br>
## Conclusion 
---
<br><br>

Data scientists and executives alike need to be thinking in terms of value creation before, during, and after AI/ML project development. Keeping the technology startup mentality in mind throughout the development process is essential for delivering that unicorn value, and in this way, data scientists and business executives can learn from new technology ventures. For more reading on AI strategy, see Cassie Kozyrkov’s post on the Applied AI roadmap [4], Silvio Palumbo’s blog on AI integration [1], and all the resources linked in the citations. It’s an exciting time to be part of the AI/ML community! Thanks for reading.

<br><br>
## Appendix: AI/ML Background 
---
<br><br>

Today’s state-of-the-art machine learning models make predictions based on patterns in historical data. These patterns correspond to correlations between model features (the dataset) and the outcome (the label prediction) and are specific to the training dataset employed. Google’s Cassie Kozykrov likens training a machine learning model to a chef learning a recipe. This is a great analogy: in the case of a Twitter sentiment model, the model is following a recipe that it “learned” about positivity versus negativity in tweets, one that is based on the factors that drove sentiment in the historical tweets at hand. TL;DR: it’s following a recipe.

An ML model is really only capable of making sound predictions on new data when things closely resemble the dataset it was trained on. This “generalization problem” is one of the most impactful, pervasive, and talked about constraints of AI and machine learning today. The ramifications: the importance of training datasets cannot be exaggerated. You need great datasets to develop AI tools. In our tooling-enabled world, most players have access to the same types of models. Common examples include XGBoost, a tree-based architecture for tabular data, and Transformers, a Neural Net architecture for natural language and computer vision. Both of these models are used by practically every player in enterprise data science. Interestingly, most of the state-of-the-art, truly massive models developed by the Microsofts of the world (the ones that are on the top of benchmark leaderboards such as <a target="_blank" rel="noopener noreferrer" href="https://super.gluebenchmark.com/leaderboard">SuperGLUE</a>  for natural language processing) are not efficient enough in terms of latency to deploy in most commercial settings. So, even though these proprietary models may appear superior if you glance at benchmark leaderboards, they aren’t efficient enough to scale in the wild. In the case of deep learning tools, often a lightweight architecture (like an open-sourced distil Transformer) can effectively do the job.

<br><br>
## Citations
---
<br><br>


[1] S. Palumbo, <a target="_blank" rel="noopener noreferrer" href="https://medium.com/bcggamma/smart-integration-four-levels-of-ai-maturity-and-why-its-ok-to-be-at-level-3-2af0c94c9614">Smart Integration: Four levels of AI maturity, and why it’s OK to be at Level 3</a> (2022), Gamma – Part of BCG X
<br><br>
[2] T. Peter, M. Blake. Zero to one: notes on startups, or how to build the future (2014), New York Crown Business (Printed Book)
<br><br>
[3] S. Berinato, <a target="_blank" rel="noopener noreferrer" href="https://hbr.org/2019/01/data-science-and-the-art-of-persuasion">Data Science and the Art of Persuasion: Organizations struggle to communicate the insights in all the information they’ve amassed. Here’s why, and how to fix it.</a>  (2019), Harvard Business Review
<br><br>
[4] C. Kozyrkov, <a target="_blank" rel="noopener noreferrer" href="https://medium.com/swlh/12-steps-to-applied-ai-2fdad7fdcdf3">12 Steps to Applied AI: A roadmap for every machine learning project</a> (2019), The Startup
<br><br>
[5] C. Taylor, D. Liu, <a target="_blank" rel="noopener noreferrer" href="https://www.youtube.com/watch?v=JkXgLyzqJg0">Using ML to tackle disruptive behaviors in gaming - Carly Taylor - the data scientist show 045</a> (2021), The Data Scientist Show
<br><br>
[6] M. Rogati, <a target="_blank" rel="noopener noreferrer" href="https://hackernoon.com/the-ai-hierarchy-of-needs-18f111fcc007">The AI Hierarchy of Needs</a> (2017), Hackernoon
<br><br>
[7] P. Nayak, <a target="_blank" rel="noopener noreferrer" href="https://blog.google/products/search/search-language-understanding-bert/"> Understanding searches better than ever before</a> (2019), The Keyword. 
 

