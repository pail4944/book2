# NetApp

Brian McKean from NetApp presented to the class a data analysis problem he'd
like to get some help on.

# Overview

Listen to his presentation carefully. Write down the answers to the following
questions to show your team's understanding of the basics of the problem.

## What is the problem?
Brian is unsure which parts of his data set are viable for further observation.

## Why is the problem important?
In order to continue his question about which SSDs to use to minimize cost, he has to pick data from systems to make conclusions. However, much of his data gives somewhat unusual amounts than what he expects. Because of this, Brian is unsure what particular data he should use for his initial question.

## What dataset has been made available?
A dataset giving dates, system serial numbers, which controller sent the data, base, observation, & delta times, and firmware and software versions was given to us by Brian.

## What specific questions are being raised?
What's the cutoff for whether something is good data or bad data?

# Q/A session

We will run a Q/A session. Before the session, compile a list of questions you
want to ask. Then, teams will take turn to ask Brian follow up questions.
Each team gets to ask one question each time. Write down the questions your team
wanted to ask and the answers you received. If another team happens to ask the
same question, simply write down the answer you heard.

## Is there any data on the number of writes?
No data on the number of writes.
## What is the ideal behavior?
One ASUP per day, per system.
## Is there any known bug with the observation time?
No, only with base time.

# Approach

Based on the information you've obtained during the Q/A session, come up with
plan how your team will tackle this problem.

## How should the dataset be imported into Tableau?
It's already a csv file, so we should be able to simply import it as a data source.

## How should the work be distributed among the team members?
We each decided to look at two questions and pick the one that was represented best in Tableau and use that one for our final report. We then reconvene with our findings to make the final report.

## What types of charts or visualizations to use to support the answer?
Mainly bar charts and scatter plots to show the differences.

## What questions may be too complex for Tableau and may require custom scripts to be written?
Questions that would need a heavy amount of data cutting and manipulation would most likely be too complex for Tableu. You can filter through the data in Tableau, but doing so may impede you from making accurate conclusions about the data.
