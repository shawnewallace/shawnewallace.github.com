---
layout: post
title: What Do You Mean by Events?
subtitle:  Understanding events and event-driven architecture and the kinds of problems you can solve.
author: Shawn Wallace
tags: [Event-Driven Architecture, Architecture]
thumbnail-img: /assets/img/eda-so-hot.jpg
---
As we stand in an era of rapid digital transformation, the way we build and interact with software systems has undergone drastic changes. New paradigms have emerged. New business capabilities have been promised. We need more efficient, flexible, and robust systems.

The emergence of agile and the effect on 'business agility' has brought new capabilities  One such approach is the event-driven architecture (EDA). Yet, many wonder, "what do you mean by 'events'?" This blog post aims to shed light on events and the event-driven architecture, emphasizing the problems this pattern can solve.

## What are 'Events'?

In the world of software, an 'event' refers to an occurrence or change in state within a system that other parts of the system can react to. It could be a user clicking a button, a system receiving a message, or a timer reaching zero. An event encapsulates an action and its associated data. In simple terms, 'events' signify "something has happened".

## Understanding Event-Driven Architecture

In a traditional system, components interact synchronously, meaning they wait for the completion of processes to move forward. However, an event-driven architecture works on an asynchronous communication model, with components acting upon events and then moving on.

The components of an event-driven architecture include event producers, event channels, and event consumers. Event producers generate events, event channels dispatch them, and


## Integration Styles
- Data-centric
- Application-centric
- Event-centric

## Events and Event Types
- State Persistence
- Data Distribution
- Notification


## Use Cases for Events
- Event Sourcing
- Event Carried State Transfer
- Domain Events
- Integration Events
- Workflow Events


## Event-Driven Architecture

### Domain vs Integration
 - Domain Events: Inside Events
 - Integration Events: Outside Events
