+++
categories= ["AI"]
tags= ["ROI", "AI", "Agile" ]
title= "Tracking AI adoption within your development organization"
date = "2025-03-16"
draft= false
+++

# Introduction

As a fractional CTO I get exposed to a lot of different development organizations.
A question I'm getting a lot recently is 'How much of our code is produced by AI'.
With today's tools this is a difficult question to answer, however, this is an 
unacceptable response considering the rising expense of AI adoption.

Simply stated we need a way to track the ROI on AI spend.  Additionally, many 
organizations have adopted multiple tools, making the question even harder to
answer.

# Possible Solutions

There are many different ways to answer this question.  As the tooling evolves I'm certain
this will get easier.

## The brute force approach

One organization I am working with is adopting a brute force approach to tracking this
information.  We have chosen to add a required field on our ticket tracking system.  This
field is required when we mark the ticket as 'Done'.  Possible choices include 'None', 'Claude',
'Cursor' and 'Windsurf' (our current AI tool choices).

From here it's relatively easy to run reports that calculate the % of tickets that utilize AI.
Additionally we can track usage by tool.  This ensures we are not paying for tooling that is not
being utilized by our team.

# Retrospective

We have set a goal to have 50% of the code we produce written by AI.  Our target to hit this goal is
6 months.  We will be presenting the utilization and trends at the beginning of each of our retrospectives.
We 'can' see this information by developer but to date have not been displaying this information during
retrosprectives, opting instead to reserve this information for one-on-one meetings with the developers.

# Conclusion

As we get more experience tracking AI adoption I will be updating my blog with approaches and outcomes.
At the time of writing this it's too early to tell if this is yielding the desired results.
