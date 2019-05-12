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

## Choose your Framework. Start and Create a New React.js Project

Forgive me. I have decided on our frontend framework for you. You are lucky. Twenty (20) years ago the framework thrown on your lap may very well have been [ColdFusion](), an interesting language to say the least. I purposely choose to not call it a dead language because the fact is they are all very much alive and in *production*, powering many applications that you probably give little thought to. I bring this up because I would like to share a few ideas before fully diving into working together using the hottest framework on the market.

1. Learning how to read, understand, and debug someone else's code and logic, is more important than understanding how to implement a new React.js application from scratch. You are more than likely going to inherit someone else's buggy application before being assign a task to implement a React.js application from scratch. To be able to debug the project in front of you to deploy it for the people who hired you, is the most valuable skillset you can learn right now. Take a look at the comments I found when reviewing the code I was given the responsibility of deploying at one of the first projects I was ever assigned as a professional software engineer:

**Buggy Application Functions**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/BuggyAF.png "Buggy App Function!")

2. When implementing a React.js application you must remember to never call `setState` from within the `render()` function or your new React Component will produce nothing but a series of infinite loops. Your render function should be a *functionally pure function* that you will use to change the view displayed to the user depending on the `state` of the application.

Now that we have a bunch of fancy backend logic on our [AWS Cloud](), we need to develop an engaging user interface that we can use to attract real *humans* to our latest *get rich quick idea*, we are going to continue to call it a digital *Wallet* to make mom, and our resume, proud. Depending


Since the [Facebook Mafia]() is much smarter than us, we are just going to go ahead and use something called [Create React App, or `create-react-app` for those who are more programatically inclined](https://github.com/facebook/create-react-app). All sarcasm and `Dilber Humor` aside, [React]() is a practical approach to another one of those esoteric software engineering questions that exist in an abundance of threads on the internet that scroll of into perpetuity. 

There was a time I had to figure out how to deploy an application into production that would allow members of a highly technical team to view and query information stored in a `PostgreSQL` database

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

#### Mobile First Styling

Next we need to configure and add the styling that Bootstrap uses and we will have to add some code to out `index.html` file to be sure that we take advantage of the standard Bootstrap v3 styles we will implement here. In your `public.html` file ass the following line:

`<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">`

Furthermore, to prevent our user's screen from zooming in automatically when they focus on an area of their device, we need to change the font size to `16px`. We need to make thee changes in the file that you can find in your project at: `src/index.css` where you will need to add the following:

```
select.formcontrol,
textarea.form-control,
input.form-control {
	font-size: 16px;
}

input[type=file] {
	width: 100%;
}
```

In the name of serving as many users as possible, we need to make sure that our application can be viewed elegantly from any mobile device above all else. With the syling above, we are trying to make sure that none of the design elements overflow off the screen to force the browser to add a scroll bar. We have to set the inputs file's width above to let [React.js]() take all screen sizes and browsers into consideration to normalize our changes across all devices for us.

### React Router for Route Handling Skills

We now need to consider a way to route the different requests that we make available to the users of our Single Page Application. We will take advantage of the nature of how components work within [React.js]() and we will use something called [React Router]() to use their collection of *navigational components* that will let us easily declare the routes that our applications needs to handle.

Lets install it first and make sure it is saved as a dependency in our `package.json`:

`$ npm install react-router-dom --save`

#### Configure React Router

We need to refactor the default files provided to us when we installed the `create-react-app` framework and we need to configure our new route-handling library so that we can encapsulate our application as a component within [React.js]() so that our application properly handle our user's requests. We need to change the `App` component in our project so thjat it looks like this:

```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';
import { BrowserRouter as Router } from "react-router-dom";

ReactDOM.render(
  <Router>
    <App />
  </Router>,
  document.getElementById('root')
);

// If you want your app to work offline and load faster, you can change
// unregister() to register() below. Note this comes with some pitfalls.
// Learn more about service workers: https://bit.ly/CRA-PWA
serviceWorker.unregister();
```

The implementation here is what enables our ability to implement and handle the routes that we need to use with our `Router` to render the `<App />` component that was initially provided to us by `create-react-app`. We also want to use the [History](https://developer.mozilla.org/en-US/docs/Web/API/History) interface in JavaScript that will allow us to manipulate our browser's session history with `BrowserRouter`. 







































