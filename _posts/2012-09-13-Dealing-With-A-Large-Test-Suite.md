---
layout: post
title: Dealing With a Large Test Suite
category: Blogging Testing
tags: blog agile tdd atdd
year: 2012
month: 9
day: 13
published: true
---
You have spent quite a bit of blod and treasure building unit, integration and automated functional testing on your project.  You take a look back and now you have 30,000 unit and coded integration tests and 1,500 cucumber features with 4,500 scenarios.  This number of tests provides an enormous amount of feedback.  Dealing with this feedback can be quite the job if it is not handled correctly.

We are experiencing a similar problem on the project on which I am currently working.  If only two percent of all of our tests experience some kind of problem in our functional test suite alone, it creates a half-day's work for two or three team members.  Each test must be manually executed and the output decoded.   There are many reasons why a test can fail but not all are bad or reproducible.  These possible questions must be answered:

   * Is it a bug (in test code or implementation)? 
   * Bad test? 
   * Bad requirement?
   * Did the browser just crash half-way thorough a test scenario?
   * Are many problems related or is this a 'one-off' issue?

We need to quickly get to the root of the any problems, get it fixed and then get it deployed.  There are a few things that we have 	done to help us wade through the junk feedback to get to the important reasons a test might fail. 

####Automate ALL test execution
Running your tests Your tests need to run automatically when you expect them to.

* Run code unit and integration tests in your continuous integration environment whenever any code is committed.
* Automatically kick off your functional test suite as often as possible as determined by your test run duration

####Make tests run fast
Tests run slowly for a multitude of reasons.  You can have a lot of tests.  You can control a lot of this by testing at the appropriate levels.  Consider the Testing Pyramid below.

<img src="/img/TestingPyramid.png" height="263px" width="313px" />

Our testing effort is divided in four distinct layers.  The number of tests in each layer should be roughly proportionate to the pyramid as tests lower in the pyramid, run quicker and are cheaper to write and maintain.  Tests higher in the pyramid are harder to write and run much more slowly.

 * __Unit Tests__ - Tests written against code with dependencies isolated.  Very fast to run.
 * __Integration Tests__ - Tests run against code with dependencies in place.  Can be slow and require setup and databases, services, etc.
 * __Functional Tests__ - Automated tests at the boundaries of system (api, user interface).  All dependencies, third-party, service etc. are in place and exercised.  Can take quite a lot of time to run.
 * __Manual Exploratory Testing__ - Performed by  testers to explore the edges of functionality.
 
These testing classifications have been written about extensively.  You can keep your test suite as fast as it can be by observing the ratios.  Write many more unit tests than integration tests.

Spread your long-running functional test run across multiple machines to ensure that feeback is timely.  We have a 60+ hour test run that we spread across 20 machines.  Our full-suite of functional tests run in about 10 hours.  The teams have their test output feedback when they come in the next day.
	
####Get your test results in a database
Lot's of tests generate LOT'S of output.  The standard HTML output from some of these test platforms can be hard to process.  Put your tests in a database.  This makes them easier to process and look for patterns of success or failure.  There can be lots of noise in test result output.  Getting it in a database will help you deal with it.  You will be able to find the important output and find ways to ignore the cruft and find the _real_ problems.

On our project, we have a custom Cucumber formatter that writes the results in a format that is easy to be imported by a process that writes them to a database.

####Give visibility to your progress
Once you have your tests running automatially and recording their output to a database, make the reporting automatic.  Have a dashboard that gives you visibility into the health of your functional test suite.  Make it easy to see what is going on.  Provide an easy way to triage any problems and rerun potentially false-fail tests.

####Deal with the output as part of your daily routine.
Running lot's of tests has no benefit unless you listen to what they tell you.  Take time at the beginning of each day to look over the dashboard and examine the test results.  Broken tests pile up quickly and you (like us) can quickly get to a point where it becomes a huge effort just to triage the backlog of broken tests.  Ensure that your functional tests pass as part of your definition of done.