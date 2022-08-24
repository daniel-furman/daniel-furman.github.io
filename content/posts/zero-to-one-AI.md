

---
title: "Why startup fundamentals are key to AI strategy"
date: 2022-08-16
katex: true
markup: "mmark"
---


# Why startup fundamentals are key to AI strategy

## Using the mentality of a technology startup to integrate AI more seamlessly in commercial contexts, 7 lessons learned from AI/ML consulting projects
---

<p align="center"> <img src="/posts/blog_AI_image_2.jpeg"/ width = "475" height = "225"> </p>

<br><br>

## Blog Post Currently Under Construction 

---

<br><br>

In his book Zero to One, Peter Thiel explores the core fundamentals that successful technology startups have in common. The takeaway: startups should exude seven pivotal traits – otherwise, queue red flags. Here's why your data science team should also exude the mentality of a technology startup to win at AI innovation, from the perspective of a data scientist in digital strategy consulting.

<br><br>

## Introduction
---

<br><br>

The parallels between technology startups and digital transformation are numerous. In both, the overarching goal is to create value through novel applications of technology. And, today, integrating AI tools is more frequently a component of digital transformation (and, as it turns out, technology startups). According to Silvio Palumbo of BCG Gamma, companies of all shapes and sizes are posed to find a "competitive advantage" through the “Smart Integration” of AI tools in the 2020s (insert Silvio Palumbo citation). 

And, while this trend is largely enabled by improvements in the open-source/subscription AI development space, the bottom-line success of AI innovation continues to hinge on value creation fundamentals (like any digital transformation). Just as the "unicorn" startup in a VC fund is more valuable than all others in the fund combined, AI models plugged into the "unicorn" use-case create more value than all other potential tools/applications/solutions combined. 

The salient question becomes: What is the most promising opportunity for AI integration given the commercial context? 

In this blog post, I argue that applying Thiel's startup fundamentals to AI development helps your team attend to that question early on and often throughout a project. Ultimately, developing tools with these seven fundamentals in mind results in products that have stronger and more consistent opportunities for value creation, the lifeline to success in AI innovation (and, usually, buy-in from executives).
<br><br>
## A primer on AI 
---
<br><br>
First, what’s AI anyways? While you’ve probably heard of Artificial Intelligence, let’s clearly define its practical meaning in digital transformation and innovation. AI refers to computer programs that automate predictive tasks. Some common examples include: What’s the sentiment of a tweet? What’s contained in an image? What’s the meaning of a phrase in a different language? For such tasks, there often isn’t a set of pre-defined rules a computer program can use to make trusted predictions. Instead, most of today’s AI tools rely on machine learning (ML) models for prediction. AI/ML tools, in the words of Google’s Cassie Kozykrov, are essentially scalable “data labelers”. 

ML models make predictions based on patterns in historical data. These patterns are surfaced during the model training phase because they are more correlated to the outcome, or label, in the given observations. Cassie Kozykrov likens training a machine learning model to a chef learning a recipe. This is a great analogy: in the case of a Twitter sentiment model, the model is following a recipe that it “learned” about positivity versus negativity in tweets, one that is based on the factors that drove sentiment in the historical tweets at hand. An ML model is thus only capable of making sound predictions in the real world when things closely resemble the dataset it was trained on. This "generalization problem" is one of the most impactful, pervasive, and talked about constraints of AI and machine learning today. The ramifications: the importance of training data for AI/ML cannot be exaggerated. 

You need great datasets to develop AI tools. In our tooling-enabled world, everyone has access to the same “near” state-of-the-art models, such as XGBoost (common architecture for tabular) and Transformers (common architecture for natural language, vision, reinforcement learning). They’re both open-sourced and used avidly across enterprise data science. The leaders of AI integration are differentiated, as a result, due to their datasets (data quality, scope, signal, commercial value, governance, importance/relevance to important business functions, etc.). The old adage “more data beats better models, but better data beats more data” is a core tenant of AI and machine learning. 

With the basics under our belt, let’s dive into how startup fundamentals can best inform AI strategy (and how I’ve employed them in previous data science projects). 

<br><br>
## Mapping startup fundamentals to AI strategy
---
<br><br>

“””

1 - The Engineering Question
It is only when you have this significant advantage in technology, that you can offer transparent superiority to the customer.

"A Great technology company should have proprietary technology in order of magnitude better than its nearest substitute."
 
Is your solution 10 times better - in a key dimension - than anything else available?

2 - The Timing Question
Are you entering an existing market with the product? Is it a slow moving market, or a fast moving one? Cleantech compared itself to the silicon chip industry of the 70’s, but failed to appreciate the speed at which that market was moving - it was expanding exponentially with Moore’s law - whereas the cleantech industry had no such advancement. There was no explosion in growth, and the industry lagged. Facebook launched at a time when broadband infrastructure was rapidly expanding, and it exploded when mobile devices and smart phones became ubiquitous. Infrastructure readiness, social norms, government regulations, established platforms and ecosystems all play a role in the timing question.

3 - The Monopoly Question
Don’t overestimate how unique your product actually is - be realistic to the competitive threats. A true innovation is one that has no competition. It has a 10X technology advancement, and is therefore clearly distinct in its space.
"Exaggerating your own uniqueness is an easy way to botch the monopoly question."

4 - The People Question
So much of innovation is about the quality of people and culture you have. And finding a technical advancement which is 10X better, means having engineers and technical people to do it. Cleantech is a perfect example, and where you find cleantech companies you would expect to find engineers running them (compare Solyndra CEO Brian Harrison and Tesla CEO Elon Musk) - but Thiel found this not to be the case. So many of the companies that pitched cleantech to him, were led by men in suits.
“This was a huge red flag, because real technologists wear T-shirts and jeans. So we instituted a blanket rule: pass on any company whose founders dressed up for pitch meetings.”
 
More broadly, you need to ask yourself if you really have the right people capable of working on real product innovations? And, do you have the best people on the team to pursue the product to market? A technical intrapreneur can lead and sell a product better than many sales people can.

5 - The Distribution Question
You might think your technology speaks for itself, but it most probably doesn’t. You still need an effective distribution channel. Primarily a way to get close to the customer, so they can experience the superior advantage you can bring.
"Cleantech companies effectively courted government and investors, but they often forgot about customers. They learned the hard way that the world is not a laboratory."
Better Place, an electric vehicle startup had the technology, but failed to market it to customers in a clear way. People were confused whether they were buying a regular car like a Renault, with added electric, or a Better Place car. It wasn’t clear what the offering actually was. The company bombed, and in 2013 when selling off the assets, they admitted they overcame the technical obstacles, but failed in the distribution ones.

6 - The Durability Question
You should plan to be the last mover in your market. What does the market look like in 10 and 20 years time? And how will your solution dominate the space? What possible competition could you face - can China make it cheaper, is the customer still ready to pay for your solution when circumstances change? You need to be asking these questions to see how durable your future is.
Cleantech relied on government subsidies and backing, which is not necessarily a durable path. It was also relying on the premise that fossil fuels were peaking as an energy source - however the rise of fracking in the mid 2000’s changed the picture, more than doubling the fracking oil industry. China became the bogeyman for US solar companies, with Abound Solar blaming “aggressive pricing actions from Chinese solar panel competitors” when it went bankrupt. Also upon going bankrupt Energy Conversion Devices filed a $950 million lawsuit against Chinese competitors for their aggressive competition.
A simple question the cleantech companies might have asked: what will stop China from wiping out our business? If there’s no good answer, perhaps the durability question was a problem.
Tesla had a head start in its field, and its design and technology is moving faster than anybody else - its lead is widening all the time. It also has a distinct and trustworthy brand, which has consumer envy. Given that buying a car is one of the biggest purchasing decisions people make, having trust in a brand is a hard thing to win - Tesla has that trust where others don’t. Similarly Apple has that brand trust, which is very hard to displace.

7 - The Secret Question
All great companies are built upon finding answers to secrets, this is the heart of innovation. Secrets are problems which have an answer, but nobody has figured it out yet. Pythagoras discovered the secrets of the triangle, Newton discovered the secrets to gravity, and NASA figured out how to land humans on the moon. These are big secrets, but every great company and product solves a problem for the customer in a new way, previously unknown. Think Airbnb and Uber.
"Great companies have secrets: specific reasons for success that other people don’t see."
Does your innovation uncover a secret, which solves a fundamental problem for the customer?
So there it is, the seven questions Peter Thiel recommends you ask yourselves. They are not easy to completely satisfy - but neither is innovation.


“””

