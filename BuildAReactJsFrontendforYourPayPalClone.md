# Part 6: Build A React.js Frontend for Your PayPal Clone

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first and second parts of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

* [Part 2: How To Configure Your Serverless Backend API](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md)

* [Part 3: How To Configure Your Infrastructure As Code, Mock Services, & Unit Testing](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigure.IAC.Mocks.UnitTests.md)

* [Part 4: How To Deploy and Configure an effective CI/CD Pipeline on AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToReviewServiceToConfigureCICDpipeline.md#part-4--code-review-deploy--configure-an-effective-cicd-pipeline-on-aws)

* [Part 5: How To Implement and Deploy your own Serverless + MicroService to AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToBuildAServerlessMicroService.md)

You can also clone a sample of the application that we will be using in this tutorial at: [PayMyInvoice B2B ClientWallet]()

Please refer to the repo above as you follow along with this tutorial. In this part of the series we will cover implementation steps for a [React.js]() *Single Page Application* that we will deploy on [AWS]() using the following [React.js]() and [AWS]() *imports* and *SDK's*:

* `react`
* `react-dom`
* `react-router`
* `react-router-dom`
* `react-bootstrap`
* `aws-amplify`

This frontend client discussed above uses the backend logic provided by the implementation of the [PayMyInvoice B2B Wallet](https://github.com/lopezdp/invoice-log-api) deployed to the [AWS Cloud]() as described in the previous chaptes in this series.

## Start and Create a New React.js Project

Now that we have a bunch of fancy logic on our [AWS Cloud](), we need to develop a pretty user interface that we can use to attract real *humans* to our money trap, I mean... *Wallet*. Since the [Facebook Mafia]() is much smarter than us, we are just going to go ahead and use something called [Create React App, or `create-react-app` for those who are more programatically inclined](https://github.com/facebook/create-react-app).

We will have to navigate out of the *serverless + microservice* project directory where we implemented our backend microservices on serverless, and we will have to create a new project we can use for our [React.js]() application. From your `home` directory, or wherever it is that you keep your project files, go ahead and create a new project by running the following command:

`$ npx create-react-app pay-me-app`

Make sure that you use the same naming convention that I have used above because `create-react-app` will not accept capital letters or `camelCase` conventions. The image below is the output you should receive from the terminal after the installation of `create-react-app` for the `pay-me-app` that we are going to developm in this part of the tutorial series.

**React.js App Success!**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/CreateReactTerminal.png "Create React App!")

Taking it a bit further, we have to verify that [React.js]() did install iteslf correctly onto our `local` machine. It's nice that the terminal says everything is fine, but it's always good to confirm right?

> "Trust but Verify." - Ronald Reagan

Go ahead and navigate into the new project directory with `$ cd ~/pay-me-app` and run the following command:

`$ npm start`

This should *spin up* the `local` resources that your need to launch your new [React.js]() application in your *browser* and you should be able to see the following generic [React.js]() application.


**React.js App Launched in Browser!**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/ReactAppBrowser.png "React App in Browser!")










