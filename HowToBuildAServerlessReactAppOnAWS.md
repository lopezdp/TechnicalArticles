# How To Build a Serverless React.js Application with AWS Lambda, API Gateway, & DynamoDB

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

### Introduction

It is amazing how quickly the technology community iterates through new technology, frameworks, and architectural paradigms to solve the never ending series of problems and *work-arounds* that a new tool, or *solution* inevitably brings to the table. Even more enjoyable to watch is the relentless chatter and online chat and commentary that spreads like wildfire all over the internet and the *Twittersphere*, that goes on discussing how to leverage the latest toolset and framework to build the next software that will **Change the World for the Better**. I must admit, although I sound cynical about the whole thing, I too am a part of the problem; I am an **AWS Serverless Fanboy**. 

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AWSServerless.png "AWS Serverless Architecture")

The objective of this tutorial is to deploy a simple application on AWS to share with you, our favorite readers, the joys of developing applications on the [Serverless Framework]() with [AWS](). The application we will be walking you through today includes a backend API service to handle basic **CRUD** operations that happens to be built on something we like to call the **DARN Technology Stack**. Yes, we created a new acronym for your recruiter to get excited about. They will have no idea what you are talking about, but they will get you an interview if you tell them you completed this tutorial to become a fully fledged and certified *Application Developer on the DARN Cloud*. The **DARN Stack** includes the following tool set:

* **D**ynamoDB
* **A**WS Serverless Lambda
* **R**eact.js
* **N**ode.js

### Toolset

For a more precise list of tools that we will be using today, below I have listed the technologies that we will be using to deploy our serverless application:

* [Lambda]() & [API Gateway]() for our serverless API
* [DynamoDB]() for our NoSQL database
* [Cognito]() for user authentication and securing our API's
* [S3]() for hosting our application & file uploads
* [CloudFront]() for serving our application to the world
* [Route53]() for our domain registry
* [Certificate Manager]() for our SSL/TLS certificates
* [React.js]() for our single page application
* [React Router]() to develop our application routing functionality
* [Bootstrap]() for the development of our UI components
* [Stripe]() for processing credit card payments
* [Github]() for hosting our project repositories