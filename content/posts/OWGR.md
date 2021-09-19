---
title: "Using Data-Driven Insights to Improve the Official World Golf Rankings."
date: 2021-09-19
katex: true
markup: "mmark"
---

# Using Data-Driven Insights to Improve the Official World Golf Rankings

---

Does the Official World Golf Rankings Ltd. (OWGR) fairly rank professional golfers? I approached this question through data mining and unsupervised learning methods with over two decades of OWGR proprietary data. Ultimately, the OWGR decided to ship ranking system updates at scale in Q3 2022 that more accurately reflect true athletic performance in professional golf tournaments worldwide. 

My background in competitive golf was well-suited to this problem domain, helping me think about ways to extend the research questions beyond the three stake-holder prescribed objectives. Here, we define the rankings as "fair" if they accurately capture relative athletic performance across professional golf tournaments worldwide, whereas "bias" is any deviation from accuracy. A problem with the current (soon to be previous) iteration of the rankings was that the system of allocating points was designed when there were significantly fewer tours included. Now there are over 20 tours with roughly 1900 athletes ranked, and the ranking system was clearly in need of a re-boot. 

Given general professional golf trends over the last two decades, I hypothesized that the rankings tended to be more biased towards premier tours relative to sub-tier tours. To explore this question, I searched for associations within the OWGR database of tournament results (16 features x 3400 obs). I first found and corrected dozens of errors across the poorly schemed relational database, issues which may have compromised our statistics. While its clear that no one can shoot "20" for 18 holes (likely a withdraw or disqualification that was incorrectly reported), its less clear if a "58" is also an error or if it was a true tournament result, and therefore extra care was taken when cleaning to ensure data accuracy. 

Many systems beyond the OGWR also require creative innovations to address today’s product questions. With this knowledge, I more clearly envision my career of scaling data-driven decision-making as a data scientist.



