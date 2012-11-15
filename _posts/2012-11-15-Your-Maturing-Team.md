---
layout: post
title: Your Maturing Team
category: Blogging
tags: centric agile
year: 2012
month: 11
day: 15
published: true
---
My high school offensive line coach always told us:

>You are either getting better or getting worse.  You never stay the same.

This is so true.  The moment you stop learning and examining yourself to get better, you begin your decline.  Often you have to take a break to get better because it's hard to improve while you are going hard.

>You never get better at your job simply by doing your job.

This is doubly true for teams.  Teams often go 'pedal to the metal' for months on end and do not take the time to self examine.  In my world we try to take this time periodically in the retrospective meeting.  Too often these meetings are necessarily tactical and do not bubble up the big ideas or are sufficiently at a low level to even see them.

Periodiocally we need to take a step back and take measure of ourselves versus our ideal or our next set of goals.  We need to see what our team looks like at the next level.  We need to mature.

####We Still Have Pain
The are some practical considerations as well.  We still have things that we are not doing very well.  In software, as we add features we rarely remove others, which brings testing and maintenance problems.  The same is true of other things that are part of our project.  We might need to scale up our teams which could trigger other changes as well.  Something we changed in our last retrospective could have surfaced some other problem or inefficiency.

On our current team environment we just shipped.  We quickly started working on another large bag of work but it is also the perfect time to self-examine and find ways to get better.  And we need to.

####Maturity process
I believe our team has done a great job.  There are few people in our area that have adopted agile practices to level we have and at this scale.  But we can _and_ do need to get better.  There are several areas in which I believe our team can mature.  Your team will probably be different, but the exercise of self-examination for improvement is a good idea.

>We're pretty good, but we need to get better.

**_True_ Test Driven Design**

We have dramatically improved our testing practices and test coverage but that was not our ultimate goal.  Our goal was to use tests to drive our design.  We will have some areas of the application that are hard to test.  Some team members use the test sometime approach which does not accomplish any of our goals. 

**Better Engineering/Design**

Improving our TDD development practice should lead us to better object-oriented design.  We have a major component that is a [God Object](http://en.wikipedia.org/wiki/God_object) and tighly [coupled](http://en.wikipedia.org/wiki/Low-Coupling_/_High-Cohesion_pattern) to multiple application layers.  This is a nightmare to test and there is redundancy.  To mature as a team, we need to have a better design approach that embraces good test-driven object-oriented practices.

**Better Craftsmanship**

We have done a very good creating features that work as the customer expects.  What we haven't done very well is to create easy to read, maintainable code.  We need to evolve our practices to think about the person who will maintain the code.

**Roll in Reporting to Show Emphasis**

We have very little visibility into the effects (positive or negative) any of our approaches.  Much of our decision making is based on [anecdotal evidence](http://en.wikipedia.org/wiki/Anecdotal_evidence).  I believe that reporting based on the data we already generate as part of our practices would help us make better informed decisions. 

**More Automation vs. Manual testing**

We do tons of automation, we need to do more.  Manual regression is expensive.  The larger the program, the more expensive the manual testing is.  We need to find ways to automate more things that can to better utilize our manual testers in ways that utilize their vast domain experience, like exploratory testing.

**Test the Mainframe (all systems in ecosystem)**

It is a fact of life that mainframes still exist in all their 1970s glory.  We have a mainframe in our world.  We send data to the mainframe, process things on the mainframe and look at the output…manually.  This is expensive.  We need to automate the manual examination of this process output.

**More pairing/less code review**

The teams have adopted a process of pairing _OR_ code review.  We often do not perform our code review when we don't pair and that has caused problems.  I am convinced that our teams would have not made certain mistakes if they were collaborating better.  Also, less shortcuts would have been taken with two people working together.

