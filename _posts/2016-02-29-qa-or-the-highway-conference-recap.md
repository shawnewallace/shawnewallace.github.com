---
layout: post
title: QA or the Highway Recap
author: Shawn Wallace
tags: [Event-driven Architecture, Speaking]
year: 2016
month: 02
day: 29
published: true
subtitle:  A summary of a talk I gave at the 2016 QA or the Highway tester conference.
thumbnail-img: /assets/img/eda.png
---
On February 16, 2016 I had the opportunity to be one of the speakers at [QA or the Highway](http://qaorthehighway.com/){:target="_blank"} in Columbus, Ohio. The following is a summary of the content of my talk.

***

I wanted to talk about microservices[^f2] from a testing professional's point of view and to discuss several potential testing approaches to assist in testing these applications.

### How we got here...
One of the goals of an agile process is to make quality a first class citizen in the software development process. We talk about testing when we plan feature development, but testing professionals are not included in the discussions when we talk about application architecture and design. This is a missed opportunity.

In the next few paragraphs, we will explore an evolution of software design from the perspective of a testing professional with the goal of giving an understanding of high level application architecture and then to provide a few options for testing them.

#### The Monolith

![](/assets/img/monolith.png)

Our applications have evolved. We started with monolithic, all-in-one systems. These systems are fairly easy to write and fairly simple to test. But as we add more code (even in a time-boxed agile process) our testing effort is always increasing.

![](/assets/img/time-to-test-vs-time-to-code.png)

When we deploy, we always deploy *everything* even if we didn't change it.

We found ourselves in a state where it is pretty easy to write code, testing is a solved problem but the time to is always increasing. Therefore getting code to production is now quite an effort in unpredictable time.

(There are also development and architectural problems with a monolithic approach to applications that we will not get into at this time.)

Our answer was to make our applications smaller.

#### Service Oriented Applications (SOA)

In moving to SOA, we broke apart our applications into their logical subsystems and treated each subsystem as a separate application. Each application now has much smaller scope and vastly less code to test. We still have the problem of an ever increasing code base, but it is more manageable.

![](/assets/img/soa.png)

Each application connects to any depedendant applications over some type of common communications structure. HTTP is very popular for this purpose. So when each application requires some functionality from another application, it simply makes a request over that common communication structure. Which led us to the dreaded 'Spaghetti Diagram.' 

![](/assets/img/spaghetti-diagram.png)

Our applications were now simpler, but their interactions were vastly more complex making testing them very difficult. We traded a tightly coupled monolith for a tighly coupled enterprise application and we did not really have the skills to test at the network layer in our testing professionals. Becuase of the tight-coupling and unknown dependencies it was still tought to test and get into production.

#### Shared Messaging Infrastructure

An answer to tightly-coupled SOA applications is to use a 'Shared Messaging' infrastructure to orchestrate the interaction between components. Applications in the system simply generate messages and await responses. The enterprise infrastrcture manages routing messages and responses.

The content of the payloads that are passed between the two are governed by the enterprise application team and agreed on as a standard of communications. These agreements are often called contracts.

Other benefits include;

* No point-to-point integrations
* Loosely coupled, highly scalable systems
* Loosely coupled TEAMS
* Easier to test
* Easier to change
* Technology flexible

Two common examples are below.

##### Enterprise Service Bus (ESB)
Systems that use an ESB utilize a software package to route messages and provide process orchestration between components.
![](/assets/img/esb.png)
ESBs can be quite effective but they are expensive, hard to maintain, require specialized skills, and are hard to test.

##### Event-driven Architecture (EDA)
An alternative approach to the ESB is EDA. In EDA, applications interact by producing and consuming messages that are distrubuted by an event channel (usually queues). Conceptually, individual applications react to events that occur in some other application by processing the resultant message. In EDA an event typically represents a "significant change in state [^f3]"

![](/assets/img/eda.png)

In these messaging based infrastructures we gain the smaller applications that we tried to get in SOA that are easier to design and test with loose-coupling between sub-systems that make it easier to test applications in isolation.

Because of the messaging infrastructure our application teams are free to build large applications or microservices, utilizing the technologies that are best suited for the job. Our enterprises can be a combination so long as all applications obey the contracts for messaging.

Many modern applications that utilize a service based architectural design pattern, will typically utilize an ESB or EDA.

#### Testing
Our approach to testing internal applicaiton functionality does not change. What does change is how we do integration testing. The contracts give us the ability to test in isolation becuase we know the format of what we produce and consume. We use the contract to test system integration at its "Edges". But these are not standard testing approaches. It is important for the tester to userstand how the applications is constructed and how they interact with each other. The tester might need an additional set of skills that are more technical in nature. Once you have developed these skills, a whole new world of testing capability becomes available to you.

##### Terminology
It becomes important for the tester to know in detail certain terminology around these design patterns.

* Http verbs and headers
* ReST
* API
* Messaging
* Contracts
* Messaging Infrastructure
* Asynchronous integration
* Loosely Coupled
* Application "Edges"
* Mocking and Faking
* Dynamic scaling
* Data consistency, Master Data Management


##### Tooling
To test these applications, we need to find their edges and test at those boundaries, by passing messages in and examining the messages that are generated. There are several tools available that aid in ths testing. These tools generally fall into two categories, manual and automated.

*Manual*

Manual testing tools allow the tester to construct messages, send then to the component and see the output. Two tools that are often used are Fiddler and Postman.

* [Fiddler](http://www.telerik.com/fiddler){:target="_blank"} - more granularity, more technical
* [Postman](http://www.getpostman.com){:target="_blank"} - more friendly user interface.	

*Automated*

Automated testing tools allow tests to be assembled into a suite and ran together without manual intervention. A common approach is to use a Domain Specific Language like Gherkin and it's most popular implemntation of [Cucumber](https://cucumber.io){:target="_blank"}.

Determining which approach will work for you team and backlog should be a collaborative effort. Spend some time researching the design patterns, terminology, and tooling and you should be better equipped to provide testing value to your team in a microservices oriented world.

The presentation materials can be found at [github.com/shawnewallace/testing-microservices](https://github.com/shawnewallace/testing-microservices){:target="_blank"}.

[^f1]: Source [QA or the Highway](http://qaorthehighway.com/){:target="_blank"}
[^f2]: Microservices: In computing, microservices is a software architecture style in which complex applications are composed of small, independent processes communicating with each other using language-agnostic APIs. (Source [Wikipedia](https://en.wikipedia.org/wiki/Microservices){:target="_blank"})
[^f3]: Source [Wikipedia - Event-ariven architecture](https://en.wikipedia.org/wiki/Event-driven_architecture){:target="_blank"}

