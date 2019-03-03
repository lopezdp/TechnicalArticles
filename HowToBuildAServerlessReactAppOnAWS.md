# How To Build a Serverless React.js Application with AWS Lambda, API Gateway, & DynamoDB

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

### Introduction

It is amazing how quickly the technology community iterates over new technology frameworks, and architectural paradigms to solve the never ending series of problems and *work-arounds* that a new tool, or *solution* inevitably brings to the table. Even more enjoyable to watch is the relentless chatter and online chat and commentary that spreads like wildfire all over the internet and the *Twittersphere*, that goes on discussing how to leverage the latest toolset and framework to build the next software that will **Change the World for the Better**. I must admit, although I sound cynical about the whole thing, I too am a part of the problem; I am an **AWS Serverless Fanboy**. 

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AWSServerless.png "AWS Serverless Architecture")

The objective of this tutorial is to deploy a simple application on [AWS]() to share with you, our favorite readers, the joys of developing applications on the [Serverless Framework]() with [AWS](). The application we will be walking you through today, includes a backend API service to handle basic **CRUD** operations that happen to be built on something we like to call the **DARN Technology Stack**. Yes, we created a new acronym for your recruiter to get excited about. They will have no idea what you are talking about, but they will get you an interview if you tell them that you completed this tutorial to become a fully fledged and certified *Application Developer on the DARN Cloud*. The **DARN Stack** includes the following tool set:

* **D**ynamoDB
* **A**WS Serverless Lambda
* **R**eact.js
* **N**ode.js

### Technology Stack

For a more precise list of tools that we will be implementing throughout the development lifecycle of this multi-part series, below I have highlighted the technologies that we will be using to deploy our serverless application:

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

### Local Development Environment Setup & Configuration

One of the more difficult activities I faced as a junior developer a very long, long, time ago was understanding that the type of project that I would be working on, very much dictated how I would eventually have to configure my machine *locally*, to be ready to develop *ground breaking and world changing software*. Anytime you read a mention to *world changing software* from here on out, please refer back to episodes of **HBO's Silicon Valley** to understand the *thick sarcasm* sprinkled throughout this article. My point is that I have always felt that most tutorials seem to skim over the idea of setting up your *local development environment*, as if it were a given that developers were born with the inherent understanding of the differences between `npm`, `yarn`, `bower`, and the never ending list of package managers and slick tools available to 'help' you succeed at this life in `SoftwareDevelopment`... For a historical perspective with a wholistic take on this matter please brush up on your knowledge of a topic some people refer to as [RPM Hell](http://wiki.c2.com/?RpmHell).

To avoid [Dependency Hell](http://wiki.c2.com/?DependencyHell), we have decided to codify and create a series of *Best Practices* you can take with you for the development of the application in this tutorial and any other projects you work on in the future. For the goals of completing the application in this tutorial please make sure to configure all `local` development machines using the tools, dependencies, and configuration parameters described in this article. This list is not definitive and is only meant as a baseline from which to begin the development of your applications as quickly and as easily as possible.

#### JavaScript Toolkit

- [ ] Node Version Manager
- [ ] Editor
	* SublimeText3
		a. PackageControl
		b. Babel
		c. ESLint
		d. JSFMT
		e. SublimeLinter
		f. SublimeLinter-eslint (Connector)
		g. SublimeLinter-annotations
		h. Oceanic Next Color Scheme
		j. Fix Mac Path (Only If using MacOS)
- [ ] AWS CLI
- [ ] Serverless Compute
	* AWS Lambda
- [ ] Infrastructure As Code
	* [ServerlessFramework](https://serverless.com)
- [ ] Package Manager
	* `npm`
- [ ] Automation Approach
	* [npmScripts](https://docs.npmjs.com/misc/scripts)
- [ ] Transpiling
	* Babel ([Included in ServerlessFramework!](https://babeljs.io))
- [ ] Module Format
	* ES6Modules (CommonJS)
- [ ] Bundling
	* WebPack4 (Included in ServerlessFramework![serverless-webpack]](https://github.com/serverless-heaven/serverless-webpack))
- [ ] Linting
	* ESLint
	* eslint-plugin-react
	* babel-eslint
	* esformatter
	* esformatter-jsx
- [ ] Testing
	* [Jest](https://jestjs.io)
- [ ] Continuous Integration Server
	* AWS CodeDeploy & CodePipeline
- [ ] HTTP Mock Framework
	* [Included in ServerlessFramework!](https://serverless.com)
- [ ] Sourcemaps
	* [Babel: SourceMap Support NPM Plugin](https://www.npmjs.com/package/babel-plugin-source-map-support)

#### Install Node.js with NVM (Node Version Manager)

On 7 November 2018, [AWS Lambda]() does officially support [Node.js v8.10.0](). This project will use [NVM (Node Version Manager)]() to work with different vesions of [Node.js]() between projects and to mitigate against any potential environment upgrades that may be implemented in the future by any 3rd party vendors. To ensure that we are working on the correct version of [Node.js]() for this project please install `nvm` and `node` as follows:

* Refer to the [Node Version Manager Documentation]() if this information is out of date
* **Installation** (Choose ONE based on your system OS):
	1. cURL:
	2. Wget:



















