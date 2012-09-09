---
layout: post
title: To the Cloud - Centric Consultings Recruiting Application
year: 2012
month: 3
day: 6
updated: 
comments: false
categories: Cloud .NET Web Development Ruby on Rails Ruby Architecture Agile
published: true
---
Each year Centric Consulting (the awesome company I work for) hosts a one day developer's conference called Camp I/O. &nbsp;This is truly a great event. &nbsp;The 2011 incarnation &nbsp;took the form of a contest in which teams were formed and a project was undertaken. &nbsp;There were lots of fabulous prizes and more importantly the 'geeks' of Centric were able to spend a day together. &nbsp;We live all over the midwest and on the east coast so this is rare. &nbsp;In all sincerity, Centric has a great community and a great group of technologists.<br />
<br />
I was happy to put together a team from Columbus. &nbsp;We decided to build an application that would assist us in the recruiting process, while highlighting our capabilities in web, mobile and testing development. &nbsp;We chose a tech stack that was unfamiliar to most everyone on the team so, on top of building an application for a contest, we were doing things that we did not necessarily do every day.<br />
<br />
First, we chose to adhere to an agile approach. &nbsp;Our time was going to be limited so if we were going to do something that provided value in the limited amount of time, we thought this was the best approach.<br />
<br />
Second, we knew that we were going to heavily utilize various cloud services so we needed to chose a tech stack that was deployable in the cloud. &nbsp;This worked well as we also had limited (read no) budget on which to support this application. &nbsp;Given that we also wanted to learn something new we chose Ruby on Rails as the core of our application. &nbsp;It deploys easily to Heroku (our Platform as a Service provider) and is open source. &nbsp;We also wrote a mobile application and service component is .NET.<br />
<br />
Third, as we were not often to co-locate, we needed to choose tools to support our work patterns and disparate development workstations (Windows, OSX and Linux).<br />
<br />
Given these constraints and goals below is a description of our tech stack and the role each component played.<br />
<br />
<b>The Stack</b><br />
<ul>
<li><a href="http://asp.net/" target="_blank">.NET</a> (C#) - We wrote service client that consume our API for easy use in integrated .NET applications.</li>
<li>Objective C - Our application included a iOS application.</li>
<li><a href="http://rubyonrails.org/" target="_blank">Ruby on Rails</a> - Is an open-source web development framework that takes web development to a new level by extending the popular <a href="http://www.ruby-lang.org/" target="_blank">Ruby</a> programming language. &nbsp;It favors 'convention over configuration' so the developer already knows how the project can be organized.</li>
<li><a href="http://rspec.info/" target="_blank">RSpec</a> was our unit and integration testing framework. &nbsp;It is widely used in Ruby on Rails projects and there is quite a developer&nbsp;community to leverage for patterns.</li>
<li>Our project team was very committed to both unit and functional testing. &nbsp;We chose&nbsp;<a href="http://cukes.info/" target="_blank">Cucumber</a> &nbsp;as a &nbsp;<a href="http://en.wikipedia.org/wiki/Behavior_Driven_Development" target="_blank">Behavior Driven Development</a> framework. &nbsp;This toolset made it possible to create executable specifications in a language consumable by the product owner and technical team members.</li>
<li>We chose a schema-less database <a href="http://www.mongodb.org/" target="_blank">Mongo DB</a>. &nbsp;Relational databases are not always called for. &nbsp;They require some level of design and mapping between an object model. &nbsp;MongoDB allows us to easily simply persist our objects with the correct level of control to tweak the persistence as needed.</li>
</ul>
<div>
<b>The Tools</b></div>
<div>
<ul>
<li><a href="http://git-scm.com/" target="_blank">Git</a> - Source Control hosted on <a href="http://www.github.com/" target="_blank">GitHub</a></li>
<li><a href="http://www.jetbrains.com/teamcity/" target="_blank">TeamCity</a> - Continuous Integration</li>
<li><a href="http://www.pivotaltracker.com/" target="_blank">Pivotal Tracker</a> - Team Board/work item tracking</li>
</ul>
</div>
<br />
<b>Design Patterns/Architecture</b><br />
<br />
<ul>
<li><a href="http://en.wikipedia.org/wiki/Model_view_controller" target="_blank">Model View Controller</a> UI Pattern is the most common UI design pattern in use today. &nbsp;Both our web and mobile ui is built using this pattern.</li>
<li><a href="http://en.wikipedia.org/wiki/REST" target="_blank">Representational State Transfer</a> (REST), simply is a way for dissimilar systems to communicate over HTTP using common HTTP verbs and text based encoding. &nbsp;In our application, we built a RESTful API &nbsp;that our user interfaces (web and mobile) consumed.</li>
<li><a href="http://en.wikipedia.org/wiki/Active_record_pattern" target="_blank">Active Record Pattern</a> is an architectural pattern for accessing and&nbsp;querying&nbsp;data abstracted in collections of objects. &nbsp;Active Record is the data access pattern built into Ruby on Rails.</li>
</ul>
<div>
<b>Cloud Services</b></div>
<div>
<ul>
<li><a href="http://www.heroku.com/how" target="_blank">Heroku</a> was our <a href="http://en.wikipedia.org/wiki/Platform_as_a_service" target="_blank">Platform as a Service</a> (PaaS) provider. &nbsp;It hosts our completed and deployed application. &nbsp;Heroku is particularly useful service and provides easy integration between many other services.</li>
<li><a href="http://aws.amazon.com/s3/" target="_blank">Amazon S3</a> was used by us to store resumes. &nbsp;This service provides a redundant and secure 'disk in the cloud'.</li>
<li><a href="http://www.sendgrid.com/features.html" target="_blank">SendGrid</a> is a great service that manages outbound email from applications. &nbsp;They provide opt-out functionality and&nbsp;deliverability&nbsp;statistics. &nbsp;Integration this service into out application was trivially easy.</li>
<li><a href="http://www.mongohq.com/" target="_blank">MongoHQ</a> is a Mongo DB cloud hosting service.</li>
</ul>
</div>
<div class="separator" style="clear: both; text-align: left;">
<span style="text-align: -webkit-auto;">The <a href="http://www.centricconsulting.com/" target="_blank">Centric Consulting</a> CampIO experience was a blast. &nbsp;I believe that the whole team benefitted from their participation.</span></div>
<div class="separator" style="clear: both; text-align: center;">
<br /></div>
