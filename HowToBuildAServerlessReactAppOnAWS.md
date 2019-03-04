# How To Build a Serverless React.js Application with AWS Lambda, API Gateway, & DynamoDB

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

You can clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer back to this repo as you follow along with this tutorial.

### Introduction

It is amazing how quickly the technology community iterates over new technology frameworks, and architectural paradigms to solve the never ending series of problems and *work-arounds* that a new tool, or *solution* inevitably brings to the table. Even more enjoyable to watch is the relentless chatter and online chat and commentary that spreads like wildfire all over the internet and the *Twittersphere*, that goes on discussing how to leverage the latest toolset and framework to build the next software that will **Change the World for the Better**. I must admit, although I sound cynical about the whole thing, I too am a part of the problem; I am an **AWS Serverless Fanboy**. 

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AWSServerless.png "AWS Serverless Architecture")

The objective of this tutorial is to deploy a simple application on [AWS]() to share with you, our favorite readers, the joys of developing applications on the [Serverless Framework]() with [AWS](). The application we will be walking you through today, includes a backend API service to handle basic **CRUD** operations that happen to be built on something we like to call the **DARN Technology Stack**. Yes, we created a new acronym for your recruiter to get excited about. They will have no idea what you are talking about, but they will get you an interview if you tell them that you completed this tutorial to become a fully fledged and certified *Application Developer on the DARN Cloud*. The **DARN Stack** includes the following tool set:

* **D**ynamoDB
* **A**WS Serverless Lambda
* **R**eact.js
* **N**ode.js

### Technology Stack

For a more precise list of tools that we will be implementing throughout the development lifecycle of this multi-part series, below I have highlighted the technologies that we will be using to deploy our application on AWS using the [ServerlessFramework]():

* [AWS Lambda]() & [API Gateway]() to expose the API endpoints
* [DynamoDB]() is our NoSQL database
* [Cognito]() provides user authentication and secures our API's
* [S3]() will host our application & file uploads
* [CloudFront]() will serve our application to the world
* [Route53]() is our domain registry
* [Certificate Manager]() provides us with SSL/TLS certificates
* [React.js]() is our single page application
* [React Router]() to develop our application routing functionality
* [Bootstrap]() for the development of our UI components
* [Stripe]() will process our credit card payments
* [Github]() will our project repositories

### Local Development Environment Setup & Configuration

One of the more difficult activities I faced as a junior developer a very long, long, time ago was understanding that the type of project that I would be working on, very much dictated how I would eventually have to configure my machine *locally*, to be ready to develop *ground breaking and world changing software*. Anytime you read a mention to *world changing software* from here on out, please refer back to episodes of **HBO's Silicon Valley** to understand the *thick sarcasm* sprinkled throughout this article. My point is that I have always felt that most tutorials seem to skim over the idea of setting up your *local development environment*, as if it were a given that developers were born with the inherent understanding of the differences between `npm`, `yarn`, `bower`, and the never ending list of package managers and slick tools available to 'help' you succeed at this life in `SoftwareDevelopment`... For a historical perspective with a wholistic take on this matter please brush up on your knowledge of a topic some people refer to as [RPM Hell](http://wiki.c2.com/?RpmHell).

To avoid [Dependency Hell](http://wiki.c2.com/?DependencyHell), we have decided to codify and create a series of *Best Practices* you can take with you for the development of the application in this tutorial and any other projects you work on in the future. For the goals of completing the application in this tutorial please make sure to configure all `local` development machines using the tools, dependencies, and configuration parameters described in this article. This list is not definitive and is only meant as a baseline from which to begin the development of your applications as quickly and as easily as possible.

#### JavaScript Toolkit

- [ ] Node Version Manager
- [ ] Editor
	* SublimeText3
		1. PackageControl
		2. Babel
		3. ESLint
		4. JSFMT
		5. SublimeLinter
		6. SublimeLinter-eslint (Connector)
		7. SublimeLinter-annotations
		8. Oceanic Next Color Scheme
		9. Fix Mac Path (Only If using MacOS)
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
	1. cURL: `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`
	
	2. Wget: `wget -q0- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`

	3. The installation will add the following to your `.bashrc` or `.bash_profile` in your `home` directory:

		```
		export NVM_DIR="$HOME/.nvm"
		[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
		[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion
		```

* Run the following command to verify the installation of `nvm`:
	1. run from Terminal: `$ command -v nvm`
	2. Expected Output: `nvm`

* On **macOS**, if you receive and error of `nvm: command not found`, then you need to add the following line to your `.bash_profile` located in your `home` directory as shown below:
	1. `source ~/.bashrc`

* To download, compile, and install a specific version of [Node.js](), then please run the following command to obtain [Node.js v8.10.0]() as needed to be able to work with [AWS Lambda]():
	1. `$ nvm install 8.10.0`

	2. You can list available versions to install using:
		* `$ nvm ls-remote`

	3. The completed output should look like this, indicating that you are now ready to start building services in [AWS Lambda]()!

		* ![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/NodeInstallComplete4Lambda.png "Complete Node Install with NVM!")

	4. Give yourself a tap on the back. Being able to hit the ground running as a new developer on a new team is a skill many employers would pay a few bucks extra to have more of on the team. Always refer to this page and tell your friends that this is where you can get the *low-down* on how to get it done without having to ask 10 questions on our favorite technology forums out in the ether.

#### Setup Editor and Install Linting

For JavaScript, React.js, and the build process that we are using in [SublimeText3]() we will proceed to configure linting, and formatting, while making use of OpenSource libraries and tools to help make this implementation of React.js more efficient. Please take the following steps to complete the installation of `ESLint`:

* **Install ESLint:** Must install **BOTH** Globally & Locally
	1. **Global Install:** `$ npm install -g eslint`
	2. **Local Install:** (Must complete from the `root` of the project directory!!!)
		* `$ npm install --save-dev eslint`
	3. **Local Install of the `babel-eslint` library also:** (Must complete from the `root` of the project directory!!!)
		* `$ npm install --save-dev babel-eslint`

* Verify that you can run `eslint` from within the `local` project directory:
	1. run from Terminal: `$ ./node_modules/.bin/eslint -v`
	2. Expected Output: `v5.15.0 (Or Latest)`
	3. Here is what the output should look like right now:

		* ![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/ESLintInstalled.png "Complete ESLint Install!")

* Initialize `ESLint` from the project's `root` directory with the following command from your terminal:
	1. `$ eslint --init`
	2. Proceed through the following wizard on your terminal:
		```
		MyDocs (master *) ServerlessStarterService
		$ eslint --init
		? How would you like to use ESLint? (Use arrow keys)
		  To check syntax only 
		❯ To check syntax and find problems 
		  To check syntax, find problems, and enforce code style
		```


































