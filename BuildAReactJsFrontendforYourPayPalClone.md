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

## Choose your Framework

Forgive me. I have decided on our frontend framework for you. You are lucky. Twenty (20) years ago the framework thrown on your lap may very well have been [ColdFusion](), an interesting language to say the least. I purposely choose to not call it a dead language because the fact is they are all very much alive and in *production*, powering many applications that you probably give little thought to. I bring this up because I would like to share a few ideas before fully diving into working together using the hottest framework on the market.

1. Learning how to read, understand, and debug someone else's code and logic, is more important than understanding how to implement a new React.js application from scratch. You are more than likely going to inherit someone else's buggy application before being assigned the task to implement a React.js application from scratch. To be able to debug the project in front of you to deploy it for the people who hired you, is the most valuable skillset you can learn right now. Take a look at the comments I found when reviewing the code I was given the responsibility of deploying at one of the first projects I was ever assigned as a professional software engineer:

**Buggy Application Functions**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/BuggyAF.png "Buggy App Function!")

2. When implementing a React.js application you must remember to never call `setState` from within the `render()` function or your new React Component will produce nothing but a series of infinite loops. Your render function should be a *functionally pure function* that you will use to change the view displayed to the user depending on the `state` of the application.

Now that we have a bunch of fancy backend logic on our [AWS Cloud](), we need to develop an engaging user interface that we can use to attract real *humans* to our latest *get rich quick idea*, we are going to continue to call it a digital *Wallet* to make mom, and our resumes, proud. Rather than get into the long history that led to React.js' role as the 'V' or the *View* in the *Model-View-Controller* design paradigm, we will spend some time implementing React.js so that you can learn by doing.  

Since the [Facebook Mafia]() is much smarter than us, we are just going to go ahead and use something called [Create React App, or `create-react-app` for those who are more programatically inclined](https://github.com/facebook/create-react-app). All sarcasm and `Dilber Humor` aside, [React.js]() is a practical approach to another one of those esoteric software engineering questions that exist in an abundance of threads on the internet that scroll of into perpetuity. Implementing frontend component in React.js is effective and more productive approach that allows you to reuse code that you have written throughout your code. React takes advantage of a [Virtual DOM]() that ituses to check against state changes to render dynamic UI elements faster than traditional MVC implementations.

### Start and Create a New React.js Project

We will have to navigate out of the *serverless + microservice* project directory where we implemented our backend microservices on serverless, and we will have to create a new project we can use for our [React.js]() application. From your `home` directory, or wherever it is that you keep your project files, go ahead and create a new project by running the following command:

`$ npx create-react-app pay-me-app`

Make sure that you use the same naming convention that I have used above because `create-react-app` will not accept capital letters or `camelCase` conventions. The image below is the output you should receive from the terminal after the installation of `create-react-app` for the `pay-me-app` that we are going to develop in this part of the tutorial series.

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

The most important part of any web development project is making sure to have a good set of tools that will let you create a beautiful user interface that your user can use to interact with your serverless backend. You can definitely spend your days implementing your own elements in JavaScript, HTML, and CSS and maybe create your own **UIKit** that you can market to the world to become famous, but for the purposes of this tutorial we are just going to go ahead and use the [Bootstrap UI toolset via the React-Bootstrap library](https://react-bootstrap.netlify.com) that we will import into each of our components as needed. We will install it and make it project dependency now with the following command:

`$ npm install react-bootstrap bootstrap`

This will make sure to add `react-bootstrap` as a project dependency in our `package.json` file that we have saved in our [pay-me-app](https://github.com/lopezdp/pay-me-app) project directory. 

Your output will look similar to the following:

```
+ react-bootstrap@1.0.0-beta.9
added 30 packages in 11.046s
```

#### Mobile First Styling

Next we need to configure and add the styling that Bootstrap uses and we will have to add some code to our `index.html` file to be sure that we take advantage of the standard Bootstrap v4 styles that we will implement here. In your `public.html` file add the following line:

`<link
  rel="stylesheet"
  href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
  integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
  crossorigin="anonymous"
/>`

Furthermore, to prevent our user's screen from zooming in automatically when they focus on an area of their device, we need to change the font size to `16px`. We need to make the changes in the file that you can find in your project at: `src/index.css` where you will need to add the following:

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

We need to refactor the default files provided to us when we installed the `create-react-app` framework and we need to configure our new route-handling library so that we can encapsulate our application as a component within [React.js]() so that our application properly handle our user's requests. We need to change the `App` component in our project so that it looks like this:

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

## Organize your App in a Container

To better organize our logic within the structure of our `App`, an ideal approach is to create a container to hold the top-level component that renders our wallet. This primary node that is the main container of our `App` will also organize the primary components that we will implement here to render the logic we need for our wallet. Before we can do that we should list a few of the views that we will need to implement to make this successful:

1. Create Invoice/Transaction
2. View Transactions
3. Pay Transaction
4. View History

The first thing we have to build is a navigation bar so that we can organize all of the views we need our users to work with. [React-Bootstrap]() makes this really easy with `import Navbar from "react-bootstrap";`. We have to make some changes to the default `App.js` file originally deployed by `create-react-app`. Take a look at the `source code` below that we need to use in the new version of our `App.js` file. 

```
/*
  Pay Me Now Wallet
  P2P anonymous payments
*/

import React, { Component } from 'react'; // Added Component
// Use Link (see r-r-d docs here), for ref to home without refresh
import { /* Link, */ NavLink, withRouter } from "react-router-dom";
// Import navbar component given to you by bootstrap 
import Navbar from "react-bootstrap/Navbar";
import Nav from "react-bootstrap/Nav";
import NavDropdown from "react-bootstrap/NavDropdown";
import './App.css';

// We need a component to "contain" our App
class App extends Component {
  // Need to render App container
  render() {
    return (
      // should probably discuss className syntax in article
      <div className="App container">
        { /* Add bootstrap Navbar */ }
        { /* probably best to discuss JSX and JSX comments */ }
        { /* collapseOnSelect - Toggles expanded to false after the onSelect
                                event of a descendant of a child <Nav> fires. */ }
        <Navbar bg="light" expand="lg">
          <Navbar.Brand href="#home">
            Pay Me
          </Navbar.Brand>
          <Navbar.Toggle aria-controls="basic-navbar-nav" />
          <Navbar.Collapse id="basic-navbar-nav">
            <Nav className="navigate">
              <Nav.Link href="#register">
                Register
              </Nav.Link>
              <Nav.Link href="#login">
                Log In
              </Nav.Link>
            </Nav>
          </Navbar.Collapse>
        </Navbar>
      </div>
    );
  }
}
export default App;
```

We are telling React that we want to use the Bootstrap Fluid Layout by configuring the `fluid` attribute, and we declare the primary `div.container` to implement a *responsive application container* with a fixed-width, so that we can add our navigation bar easily. We also have to figure out a way to get our users back to the homepage without triggering a refresh event. To get our users to their homepage dashboard we are going to use React-Router's `Link` component to get us there. Finally, we need to begin to style our application. Please copy the following `css` styling to the same directory as your `App.js` script in your project directory, and call the file `App.css`.

```
.App {
  margin-top: 15px;
}

.App .navbar-brand {
  font-weight: bold;
}
```

### Implement your landing page

With the primary application container ready, we need to implement our landing page in a `Home` container that we can use to respond to the `/` route where our primary components will live, and that we can use to make requests to our serverless + microservices. We will want to differentiate our primary containers from the rest of the components in our application, and we will use `$ mkdr src/containers` from our project's root directory to save these files.

Now that we have structured our application properly, we can complete the first iteration of our landing page so that we can show something to the rest of the world. Create a new file called `Home.js` inside of the `src/containers` project directory. All of the primary containers that provide our routes with a response, and that will send requests to our serverless backend, are just the primary views that our user interacts with in our application. Take a look at the file we have implemented for you in the `src/containers/Home.js` project directory and make the changes in your project as needed. Below is what we completed for this tutorial:

```
import React, { Component } from "react";
import "./Home.css";

export default class Home extends Component {
  render() {
    return (
      <div className="Home">
        <div className="landing-page">
          <h1>UPay Simple. A Secure Wallet</h1>
          <p>
            A simple & Anonymous P2P payments app.
          </p>
        </div>
      </div>
      );
  }
}
```
Slowly we make progress. Here you have rendered your first `html` page using [JSX](), an extension to JavaScript that lets you use an `xml`-like syntax in the views that you implement to elegantly describe what you want your user's interface to look like. Here is the magic that we find in React; it embraces the fact that the logic required to implement an elegant user interface is tightly coupled with rendering, state changes, data preprocessing and application logic also. React allows you to create simple components that let you separate architectural considerations efficiently, to help you feel more comfortable writing your `html` markup into your JavaScript functions, so that you can more easily render the views you need to your users. 

The `JSX` we are rendering above is only going to display the first version of our homepage to the users of our new Wallet. Copy the `css` styling below into the `src/containers/Home.css` file in your project directory so we can start making this page look presentable:

```
.Home .landing-page {
	text-align: center;
	padding: 65px;
}

.Home .landing-page h1 {
	font-weight: 700;
	font-family: sans-serif, "Roboto";
}

.Home .landing-page p {
	color: #999999;
}
```

### Configure your Application's Routing

Now that we have a `Home` page component that we can use to start displaying some form of content to our user, we need to configure the routes that our application will use so that the view implemented above, can respond appropriately when a user triggers an event that calls the `/` route from anywhere in the application. We will use `react-router` and the `Switch` component it gives us, to render an *exclusive* route that we can display to the user as the first resource defined within the component, that precisely matches the path we need. 

Review the code we implemented below that you need to create as a new `src/Routes.js` file in the project directory and add the following to your implementation:

```
import React from "react";
import { Route, Switch } from "react-router-dom";
import Home from "./containers/Home";

export default () => <Switch>
                       <Route path="/" exact component={ Home } />
                     </Switch>;
```

Taking a look at this a bit deeper, you can see that we are using the `exact` property because we **must** precisely match the `/` path defined as a route in our implementation file. Using the `Switch` component forces us to use the `exact` prop like this because it will force the `/` route to match every route that uses the `/` at the start of its declaration.

### Display your Home Container Route

We need to refactor our `App.js` component so that it knows how to properly respond to the events triggered by a user who is requesting a particular route from our application. We need to add the `<Routes />` component that we implemented above so that our user can navigate through the different features that we will provide them with to make and accept P2P payments from within our application. Take a look at the updated `App.js` source code below that you need to be sure to implement in your own project:

```
import React, { Component } from 'react'; // Added Component
// Use Link (see r-r-d docs here), for ref to home without refresh
import { Link } from "react-router-dom";
// Import navbar component given to you by bootstrap 
import { Navbar } from "react-bootstrap";
// Import Routes component so that App knows how to 
// respond with correct view
import Routes from "./Routes";
import './App.css';

// We need a component to "contain" our App
class App extends Component {
  // Need to render App container
  render() {
    return (
      // should probably discuss className syntax in article
      <div className="App container">
        { /* Add bootstrap Navbar */ }
        { /* probably best to discuss JSX and JSX comments */ }
        { /* collapseOnSelect - Toggles expanded to false after the onSelect
                event of a descendant of a child <Nav> fires. */ }
        <Navbar fluid collapseOnSelect>
          <Navbar.Header>
            <Navbar.Brand>
              <Link to="/">
                Pay My Wallet
              </Link>
            </Navbar.Brand>
          </Navbar.Header>
        </Navbar>
        <Routes />
      </div>
      );
  }
}
export default App;
```






... 



































