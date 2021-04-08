---
layout: post
title: LIME App Design
categories: webapps
---

## What is LIME?

LIME is a real-time chat application that I am working on, which I am using to practice some skills for myself. It's not at all meant to be a "real" product; rather just something for me to practice skills that I don't touch all that much in my day job. Also, I think it's pretty fun to be honest.

In this post, I'm going to outline the current overarching design/architecture for the project (subject to change as we go, of course), including the technologies in play.

So let's hop to it!

## High-Level Design

### Requirements 

So first, we need to think about, at a high level, what we're trying to achieve. And then we can work out, at ever-increasing levels of detail, how we will achieve that. To that end, I laid out some requirements that LIME *must*, and *should ideally*, meet:

- LIME *must* permit real-time communication
- LIME *must* permit users to have persistent accounts
- LIME *must* store and transmit its users' data securely and in a GDPR (Data Protection Act 2018 in the UK) compliant manner
- LIME *must* permit users to create "rooms" to provide access-controlled communications
- LIME *should ideally* allow google account login
- LIME *should ideally* allow users to PM each other
- LIME *should ideally* permit users to send files and images and video to each other
- LIME *should ideally* be able to scale out and scale in as appropriate to current load.

### Overall Architecture

With these requirements in mind, I quickly decided that I'd like to build LIME using a (micro)service-oriented approach. This would reduce the size of the individual codebases, thus reducing cognitive load on myself, and would also make it easier to work in different frameworks and languages where appropriate. Having separate services also has the usual benefits of better encapsulation, easier scaling, etc.

The next question is: what will the services be? These are the services which come to mind:

- An auth service, to check user identities and permissions
- A user info service, which will hold users' profiles and such
- A messaging service, to handle the core text messaging
- A file-upload service, to handle storage of files which are uploaded
- A frontend
- A "rooms" service, to store data associated to individual rooms

## Lower-Level Design

### Technologies

I decided that, in order to expedite things, I'd stick to using Java and the Spring framework for the backend, since I am familiar with those from my day job. For the frontend I would use whatever.

All the services will run in Docker containers in order to allow us to use e.g. Kubernetes to provide easy (horizontal) scaling. For ease and cost reasons, the services will be deployed to Heroku during development, and at the end of the project I will put together some Terraform scripts and set it up so that it *can* run in AWS if I wish (though cost would probably make that prohibitive except for a short proof-of-concept deployment).

Source control will be GitHub, and CircleCI will be used for CI/CD, since they seem to have good support for building and deploying Docker containers.

The databases will be Postgres, using the free DBaaS provided by Heroku (and once we shift to AWS we'll stand up Postgres instances in RDS).

### Interfaces

The following diagram illustrates the interfaces between the services:



The following table provides some implementation notes about these interfaces:

| Interface | Data Format Notes | Security |
| -- | -- | -- |
| Frontend to Auth | REST requests, using JSON | TLS on the connection |
|||
