# Intro
- Introduce self - Associate Directory of CI and Assoc Dir of Synthesis
-- what are your roles, how do you interact w/ groups.
- Helping researchers use data effectively to make discoveries and advance science is something we're passionate about and do a lot of
- So we're excited to have this opportunity to talk with you about how to introduce that early to future researchers and 
make that part of the undergraduate curriculum. 
- A quick note about the format and structure of the workshop: We'll start with a brief talk to frame some of the issues as we see them and then devote most of the time to hands on exercises with tools.
- We want to keep this workshop informal and give you plenty of opportunity to ask questions, talk about your ideas and concerns, and connect with each other around the issues. That said, we'll reserve the right to intervene to keep the workshop focussed and maintain.

# Overview
- Why we're here
- What is sesync? what do we do
- Where does big or not so big data fit into this?
- Start coding

# Goals

- We want you to think about how would you adapt that bit that we teach today with your current cirriculum. 
- Teaching with data, hands on and by example is how we've found this works best. DOes this type of teaching hold true for undergrads?

# Who are we
- SESYNC is funded by a grant from NSF to the University of Maryland. We provide various kinds of support for new interdisiciplarny collaborations of social and natural scientists from around the world to advance research at the nexus of humans and the envioronment.
- All of our 85+ supported teams use existing data sets - we don't fund new data collection
-- Well mostly, we have had a postdoc study our groups in an attempt to further the understanding of team science
- One of the critical types of support we provide is cyberinfrastrucutre. We have a small computing cluster on site which allows teams to do data processing on  scale that's bigger than powerful PCs but not so big as supercomputing.
- We've found many of our teams need to reconcile, integrate, synthesize many different kinds of data from many different sources, often messy data. And often times, they don't know where to start.
- So for the last couple of years we've been running hands-on training workshops to help them get up and running.
- These are skills and approaches which are rarely taught in undergraduate or even graduate programs.

# What is big data?
- Big data is a term that's thrown around a lot and frequently causes a lot of eye rolling
- We are going to reframe and actually broaden out to address the entire context of data science, because working with big data is a subset of the skills and mindset of data science. And having some knowledge of the big picture of data science is 
really a prerequisite to working with big data.

# Data science
- This is a popular Venn diagram which visually summarizes where data science fits in the landscape of familiar domains
- All faculty have substantive expertise, and this is the core of what you teach to your students about your disciplines.
- The importance of Math and statistics is widely accepted to conducting empirical research in all scientific domains. For undergrads, who may not want to go into research, the analytical ability and skills which that encompasses have been highly sought after by employers and are transferable to many pursuits.
- So what's the role of hacking or programming skills? In the digital age, to effectively answer substantive, empirical questions requires knowing how to use computers to find, acquire, structure, clean, summarize, analyze, and present data.
- It doesn't mean needing a degree in computer science, but it does mean having a feel for the computational processes and tools that underlie each of these steps. The more hacking skills one has, the more one is able to control this process.
-- In fact, having a CS degree doesn't necessarily you know how to program practical things
- We figure most folks in this room are aiming for their students to land here.


# Research Process
- Taken as a whole, these verbs as the core part of the research process once you have a question you want to answer. Many of you already incorporate some of these into your teaching. Perhaps you give students a data set and ask them to summarize, analyze, and graph the data it contains.
- We think this framing helps put those steps in the context of the research and discovery process and gives students an idea of what they'll have to deal with when they go to apply classroom knowledge in other contexts.
- So, during the workshop we are going to touch briefly on some tools and considerations for each of these. We'll actually start with the second one and come back to web data at the end since it is the topic that is probably most new to everyone and we'll have some context for how/where you might work wiht that.
(#2)
- We won't get heavily into statistics but will stay focussed in the "hacking" regions, because these are where the challenges are in terms of developing the mindset of a data scientist and in tackling big data from the standpoint of domain social science.

# Big Data: Promises and perils
- Before we move into the hands-on exercises, I'd like to spend a few minutes talking about data generally, where it comes from and what we do with it in the hopes of planting a seed in the back of your mind. Because as we go through the tools, we want you to be able to connect what they *can* do to what you already know and what you want them to do, what you want to get out of them, how they might be able to provide insight and meaning and particularly how they could spark that aha for your undergrads.
## Data structures
- Let's take a poll: how many people have worked with tabluar data? Vector data? Raster data? Unstructured data? Some other kind?
- There's a massive increase in not only the size of data but also the sources, formats and structures of data. Being clear about issues like: where did the data come from? how reliable are they? what might the biases be? what unit of analysis do I want and how do I get to that? -- these are all critical parts of the analysis process, regardless of if you're using a short survey of 100 people or millions of tweets to answer a question.
## Prediction v. causation
- As scientists, most of the time you are, I think, interested in causation, in explanation, in looking at the reason why humans and their institutions behave in the way they do and make the choices they do.  A concern that many scientists express about big data is that there's little in the way of theory or explanatory power in the algorithms that are employed to make sense of it. And that's true. 
- So it's worth considering, when is explaining causation necessary v. when is making accurate predictions sufficient? This is particularly relevant for undergrads who may not be going on to graduate school but will be employed at companies or as practitioners or even researchers.
-When a company employees big data analytics, they aren't necessarily interested in understanding why a customer makes a purchase, they simply want to be able to predict their future purchases. And this is true in places outside of corporate America: a police chief would likely be satisfied knowing where the next crime would occur without an explanation as to why.
- At the same time, there should be a realizatioin that just outcome may be correctly predicted, there is not necessarily a deeper understanding into the conditions or processes that made it so.
- There are also ethical issues of privacy, of whether or to what extent the characteristics of individual's or their past should be used to make predictions or decisions about their future. Parole departments in some places, for example, are using data about reoffending and offender characteristics to make decisions about who should be released.
## Visualization
- Finally, visualizing truly large or messy data sets can lead to new insights that may not otherwise 
- Your eyes are a good spot checking mechanism for finding outliers.
- choosing the right and honest visualization

# Process scaling at sesync
- These are a few ways in which we help researchers scale their analysis at SESYNC. 



http://api.dhsprogram.com/rest/dhs/data?breakdown=national&indicatorIds=20171000,70254002,127383002&returnFields=Indicator,CountryName,SurveyYear,Value&f=json
