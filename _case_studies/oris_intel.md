---
layout: post
title: "DRAFT: Centric Partners with Oris Intel"
categories: project architecture
author: Shawn Wallace
tags: blog
year: 2016
month: 9
day: 23
published: true
summary: A summary of a project that we did for Oris Intel
date: 2016-09-24 05:00:00
---

#### The Business Need
[Oris Intelligence, LLC](http://www.orisintel.com/) provides Minimum Advertised Price (MAP) monitoring and enforcement tools for product manufacturers. They 
monitor public product listings for thousands of products across hundreds of websites and generate reports for the manufacturer. Their business 
is growing rapidly and at scale. While Oris Intel provides the data and analytics of the monitoring output, they relied on third parties 
to provide the raw data they required. System volume was large: 200,000 products needed monitored every three hours.

* They needed to increase the volume by orders of magnitude
* The expansion would come very quickly
* Needed to reduce dependency on third parties for core functions
* Wanted to improve and control reliability
* Needed the ability to add additional solutions for monitoring different kinds of sites
* Better scaling options
* Improve the timliness of adding new proudcts. The current product backlock was estimated at about a year. 

Oris Intel decided to add the monitoring capability to their core technical competency. While Oris Intel constructed and maintained their 
data and analytics platform, they did not have the current staff to design and implement the new application product offering.

#### Enter Centric
Oris Intel partnered with Centric to provide a team of an architect and application developers to build out the initial versions of their 
MAP monitoring infrastructure. Features include:

* Basic site monitoring features in production and monitoring sites
* Marketplace specific functions
* Strategy for dealing with custom monitoring use cases
* Ability to collect important meta-data from the sites
* Persist data for manual use
* Build with a monitoring infrastructure to track and manage system exceptions
* Scaling infrastructure in place
 
#### Project Summary
Centric and Oris Intel together created a scalable microservices-based design utilizing asynchronous messaging approach. The approach:

* allows dynamic scaling of the production environment, application-by-application
* adds ability to create new applications to perform additional MAP monitoring capability without changing infrastructure
* embraces common DevOps practices to provision, test, deploy, and monitor the applications in production
* utilizes an open-source technical stack
* is fully cloud deployed

#### Results
Oris Intel is now able to address their existing backlog and add new products quickly. They can scale to the business volume according to their
own capacity planning model and adapt to the resulting technical scale without having to depend on external partners. Utilizing Centric, Oris Intel
was able to add new capabilities while they were ramping up the size of their organization. The resulting architecture provide a 
very good foundation for future growth.

