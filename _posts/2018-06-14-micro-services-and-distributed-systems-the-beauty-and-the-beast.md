---
title: 'Micro-services and Distributed Systems: The Beauty and the Beast'
layout: post
subtitle: 'A jouney to understanding the concepts behind microservices through my own perspective as an explorer of the wild realm'
image: http://manzzup.github.io/blog/public/images/4/ms-00.png
---

This is not going to be one of those blogposts that would sugarcoat some buzzwords and leave you with nothing but some bullet points at the end of the article. 

NO.

After designing 3 fully functional microservices architectures (one co-designed with @lahirudealwis ) that are functioning smoothly as ever (very much of an achievement), I decided to write the following post. The goal is to provide an introduction to microservices for engineers using my own path of exploration. I believe that rather than reading on microservices on countless posts, articles and tutorials, a guided introduction would help someone to bootstrap the process.

When I was starting with micro-services, it's pretty much confusing to realize what is what (semantically incorrect but you get the idea). ___Later on I found that reading about microservices is not the exact way of knowing microservices, but rather exploring is.___ What's going to follow in this article is a summarized and structured view on my journey of discovering microservices and the many wonders of it. Yes, distributed systems are also there and it is merely not a keyword.

The big three questions I had on microservices was
1. What?
2. Why?
3. How?

The issue was trying to explore this top to bottom, so let's take the bottom first

## HOW?

How is pretty easy, as the name says those are micro services. But what is a service? what's so micro about it? Most importantly us engineering just want to know how the hell we design such systems? 
Let's dive in with a demo scenario.

### Scenario

> A system, where users upload big data sets (let's say ~100MB a piece, no streaming but bulk uploads) containing transaction records. The system in return analyse these data (using cutting edge machine learning stuff) and emails the results to the user. Also users can query for their results and data through an endpoint.

You being the enterprise systems guy, comes up with the following system architecture.

![Monolithic architecture](/public/images/4/ms-01.png)

This looks good, but now when Joe, your PM wants you to move to micro-services architecure (mostly because it sounds better with the upper managment), you need to redesign the whole thing. So you wonder, what defines a "service"?

> A service is a single functionality of the system that could be made to function independently without regarding the rest of the components. 

If we think about the **MailClient**, what the hell does it has to do with the DataProcessor or infact any of the other components? NOTHING. It just need to know what data to be sent in the email body and whom to send the email and do exactly that. So we found our first service, the **Mail Service**. Extend the same thinking to the rest of the components and BAM! we have 4 services.

1. Mail Service
2. FileUpload Service
3. Query Service
1. DataProcessor Service

What about the Data Layer? 

We can but practicality dictates that the communicating data read / write requests as messages gonna be a hell of a bottleneck on the overall system. A better choice is to host each database independetly and let the underlying hardware network handle all the message passing. 

Here's my design for the above system, but keep in mind it is ONLY a design and no way suggest that it is the optimal solution.

![Micro-services architecture](/public/images/4/ms-02.png)

Is it just me or the shit looks a bit ugly now?

Yes, because some services still need to communicate a bit with other services. Does this mean our initial breakdown of the services is wrong? No, services are meant to be communicating, but aggregating services depending on the level of communication is a design decision. However, in order to tacle our current problem, we introduce another component, we call it the **API Gateway**.

![Micro-services architecture with API Gateway](/public/images/4/ms-03.png)

*sigh* much better. Now each service simply asks the **API Gateway** to tell the other service to do their work. I guess this gives a very abstract view on how to convert a monolithic system to a micro-services "oriented" system. 

As it can be seen, the system now is seggregated into beautiful pieces that can be developed, deployed and tested individualy while keeping the same coupling and communication as of the monolithic system. Hence microservice is the *Beauty* of the equation.

This does not convey actual implementation details, but I hope to dive into it in a latter post. Now that we know how, let's see why?

## WHY?

Consider the original monolithic design; one fine morning Alice your Sysadmin barges in and screams that the system is overloading because the data processor is taking up all the resources to analyse some dataset. And the system needs to send out 1 million emails at the same time. You want to scale up, but it seems impossible to scale up just the two component without affecting the other activity. 

On the other hand what if one component fails and the whole system shuts down without a warning? How do we introduce fault tolerance and load balancing. While this do not insist that monolithic system can "never" has such features, this is a way of thinking that led to the microservices path.

Now consider our latter design based on microservices; yes the services are isolated. One shutting down will not affect the other. But how exactly it helps with scaling up? because the picture above does not introduce the *Beast* of microservices, **Distributed Systems**

Just like Micro Services, Distributed Systems has a trivial meaning. Systems are Distributed. Let's take a look at our microservices in a slightly different perspective.

![Micro-services architecture with distributed nodes](/public/images/4/ms-04.png)

node 01 - 03 are separate systems of the same network. But now the functionality and issues of one node does not affect the performance of the other. PLUS we could simply increase the number of services (scale up) by introducing new nodes at any point of execution. This simply brings out the true power of distributed systems.

> Microservices are a way of implementing Distributed Systems. It hardness the power of distributed systems to provide scalability, realiability, high availability, and other soothing words.

I think why microservices is clear now. Apart from these obvious use cases, microservices enables Agile development by making the system inherently compatible for modularized development. Which in turn makes the lives of QA peeps easier, now that they can test each service separately not worrying about what else is broken in the latest release.

Which leaves us with what.

## WHAT?

As i mentioned earlier, I believe that the question "what is microservices" is now made clear. 

>Microservice is a system design pattern / architecture that enables modularized systems that can be deployed in a distributed manner.

## Tl;Dr

The goal of the article was to provide a bottom up approach in understanding the microservices and the role of distributed systems in it. 

>Microservice is the Beauty, since is provides the elegant system designs that are modularized, isolated, agile but powerful,  Disributed Systems is the Beast that powers up the services providing scalability, reliability and robustness.

In my experience, a microservice architecture design starts with a monolithic design, which is then modularized to identify the services. While this article provides an abstract view on the microservices concept, it hardly touches the actual design implementations of such systems. I highly recommend the [Pragmatic Microservices by Kasun Indrasiri](https://medium.com/microservices-in-practice/microservices-in-practice-7a3e85b6624c) for further reading to grasp a better understanding. 

In the proceeding posts, I hope to dive into more practical aspects of microservices such as service containment, distributed messaging, distributed logging, container deployment and mangement etc. It's a long list but since my current interst area lingers here, I'm hopeful :)

Till then, have fun with microservices!