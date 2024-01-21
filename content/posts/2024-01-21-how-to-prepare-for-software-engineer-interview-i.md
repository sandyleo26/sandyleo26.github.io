---
title: How to Prepare for Software Engineer Interview - System Design I
date: 2024-01-21
enableGiscus: true
tags: [me, interview, job]
---

In my last blog, I talked about how to prepare for software engineer interviews. To summarize, you need to prepare for questions in 3 big categories: behavioral questions, coding and system design. Each category deserves a few articles to elaborate. In this article I'm going to deep dive in to how to prepare for system design questions.

## What is System Design Question

A system design question looks like "Let's build a service that allows user to post short messages and follow each other (build a twitter or X)". Or "How to build a service that allow people to upload and view videos (build a YouTube)". Obviously, it's impossible to design a service that took thousands of engineers decades to build so in practice the interviewer will focus on a few core features or scenarios. For example, the when asked to design a twitter, you probably only need to design the posting service and how to follow and unfollow people.

In my experience, I've never been asked to design a well-known commercial service. Most of time, the questions are about problems that the interviewer has solved or (been working on). For example, in one interview, I was asked to design a system that monitors a fleet of a million databases. In another interview, the interviewer asked me to design a service that allows user to comment and "like" a video. In both cases, the questions are related to the area the interviewers are working on and both questions are about a particular feature or sub-problem of a product.

## How to Answer System Design Questions

Here are a few key steps you should follow when answering system design questions

0. Clarify requirements
1. Draw a high level architectural diagram
2. Discussing API and database
3. Discuss core and edge cases
4. Discuss scalability

### Clarify Requirements

There're two categories of requirements: functional and non-functional requirements. Functional requirement is like "should I design the twitter direct messaging function and user login part or not". These requirements are about what functions of a service that the interviewers are trying to test you. Non-functional requirements are more related to the scale of the service such as "what QPS should I have in mind when design this service" or "how much storage I need to store all the information in a week/month/year". If you're designing twitter for under 100 users, then a single machine could do it all.

Functional requirements decide what you design and non-functional requirements decide how you design. Without having a good understanding of the requirements, you are destined to fail. So we need to ask clarifying questions first when we receive the questions about anything that could impact your design.

### Draw a High-Level Architecture Diagram

This is an easier part. Before discussing any implementation details, draw a diagram to illustrate your design from a very high level and only cover the simple scenario.

![system design diagram](/system-design-diagram.webp)
_source: https://qr.ae/pK6GcL_

It's easy because most designs look very similar on a high level, especially if it's backend design problem. Doing this allow the interviewer to see into your brain instead of relying on verbal description. This is especially useful if English is your second language. The diagram will be also useful in facilitating the follow-up discussion.

### Discuss API and Database

API design and database schema design are the core parts of any backend system therefore these two areas are usually what interviewers want to focus. API designs impacts frontend the most while databases impacts your backend. Have a good design will make integration easier and more adaptive to future change. Both can be used to access your skills at translating a business problem into a data modeling problem. As with any skills you can improve them  doing lots of projects and learn what works and what not. It's hard to fake it if you haven't worked on any projects building APIs and writing SQL queries.

### Discuss Core and Edge Cases

After you have the diagram, API spec and database schema, it's time to do a simulation using those and demonstrate how your proposed design to satisfy the requirements.

The difficult part usually comes when discussing edge cases. This is usually where the real battle happens. Sometimes the interviewers mention the edge cases upfront and sometimes they will watch you fall into their trap and then ask you some follow-up questions. For example, in design twitter, the interviewer might ask you how to handle user who follow thousands of people. How to make sure such users can get the latest posts from their followees without killing the database. Like most system design questions, there's no right or wrong answer but you need to elaborate on your design: what are the pros and cons and how to mitigate cons. What are the assumptions you've made and whether those assumptions are reasonable. You need to come up with alternatives and compare it against with the other.

### Discuss Scalability

This part is also easy and straightforward because there are limited set of questions and answers. For example, when asked how to speed up queries, the answers will almost always be use replica or cache. If it's to speed up write queries, then think about sharding your data or use SQL databases that has a flat curve of latency vs QPS. If it's about handling surging request, then make sure to mention using a message queue flatten the request peak.

## Conclusion

We talked about what is system design and the general steps to follow when answering those questions. In the next post I'll talk about how to actually prepare for it.
