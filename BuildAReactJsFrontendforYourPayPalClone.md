# Part 6: Build A React.js Frontend for Your PayPal Clone

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first and second parts of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

* [Part 2: How To Configure Your Serverless Backend API](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md)

* [Part 3: How To Configure Your Infrastructure As Code, Mock Services, & Unit Testing](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigure.IAC.Mocks.UnitTests.md)

* [Part 4: How To Deploy and Configure an effective CI/CD Pipeline on AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToReviewServiceToConfigureCICDpipeline.md#part-4--code-review-deploy--configure-an-effective-cicd-pipeline-on-aws)

* [Part 5: How To Implement and Deploy your own Serverless + MicroService to AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToBuildAServerlessMicroService.md)

You can also clone a sample of the application that we will be using in this tutorial at: [PayMyInvoice B2B ClientWallet](https://github.com/lopezdp/pay-me-app)

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

This should *spin up* the `local` resources that you need to launch your new [React.js]() application in your *browser* and you should be able to see the following generic [React.js]() application.

**React.js App Launched in Browser!**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/ReactAppBrowser.png "React App in Browser!")

### Small Changes 

If this is your first [React.js]() application, we can understand why you may be so excited about the output on your browser right now. But where do you start? Let's keep it simple, and change the title in our application's `index.html`. Navigate to:

* `$ cd ~/pay-me-app/public`

Open the `index.html` file in the project directory and edit the `title` tag so that we can name our application accordingly. Below is how I named my version of the application locally:

`<title>Pay Me - An online general ledger to track your income.</title>`

You can see the changes made at the repository we have created for you on GitHub for the [pay-me-app](https://github.com/lopezdp/pay-me-app).

[Facebook]() did a wonderful job with the [Create React App] framework to make it easy for us to quickly get started with any frontend project. They packaged an easy to use, and compact development library that includes tools that we can use to enable testing, refreshing our app when our files change, by restarting our app in the background, and it also includes ES6 support. 

### UIKit with React-Bootstrap

The most important part of any web development project is making sure to have a good set of tools that will let you create a beautiful user interface that your user can use to interact with your serverless backend. You can definitely spend your days implementing your own elements in JavaScript, HTML, and CSS and maybe create your own **UIKit** that you can market to the world to become famous, but for the purposes of this tutorial we are just going to go ahead and use the [Bootstrap UI toolset via the React-Bootstrap library](https://react-bootstrap.github.io) that we will import into each of our components as needed. We will install it and make it project dependency now with the following command:

`$ npm install react-bootstrap --save`

This will make sure to add `react-bootstrap` as a project dependency in our `package.json` file that we have save in our [pay-me-app](https://github.com/lopezdp/pay-me-app) project directory. 

Your output will look similar to the following:

```
+ react-bootstrap@1.0.0-beta.8
added 30 packages in 11.046s
```

























