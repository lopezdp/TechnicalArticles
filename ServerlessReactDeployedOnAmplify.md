# Part 7: Integrate your serverless + microservices with React.js and deploy your App on AWS-Amplify

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first and second parts of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

* [Part 2: How To Configure Your Serverless Backend API](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md)

* [Part 3: How To Configure Your Infrastructure As Code, Mock Services, & Unit Testing](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigure.IAC.Mocks.UnitTests.md)

* [Part 4: How To Deploy and Configure an effective CI/CD Pipeline on AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToReviewServiceToConfigureCICDpipeline.md#part-4--code-review-deploy--configure-an-effective-cicd-pipeline-on-aws)

* [Part 5: How To Implement and Deploy your own Serverless + MicroService to AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToBuildAServerlessMicroService.md)## Part 6: Build a React.js Frontend for your PayPal clone. Take home the Cash with the PayMyInvoice App!

* [Part 6: Build a React.js Frontend for your PayPal clone](https://github.com/lopezdp/TechnicalArticles/blob/master/BuildAReactJsFrontendforYourPayPalClone.md) - *Not Published.*

You can also clone a sample of the application that we will be using in this tutorial at: [PayMyInvoice B2B ClientWallet](https://github.com/lopezdp/pay-me-app)

Please refer to the repo above as you follow along with this tutorial. In this part of the series we will continue to cover the needed implementation steps for a [React.js]() *Single Page Application* that we will deploy on [AWS]() using the following [React.js]() and [AWS]() *imports* and *SDK's*:

* `react`
* `react-dom`
* `react-router`
* `react-router-dom`
* `react-bootstrap`
* `aws-amplify`

## Implement User Permissions and Registration

Now that this application of ours has a login interface that our users can use to authenticate themselves, we are going to have to make sure that there is a mechanism in place to enable the permissions our users need to create and manage their transactions within our app. To properly complete thes configuration steps we will need to be able to load our application's current state from our user's login session managed by Cognito, we'll need to implement a few redirects for proper login and logout functionality, and more importantly we always have to make sure that we are giving our users good feedback when logging in so that they can be sure that they are submitting the correct credentials.

Initially we really need a way to update the application state when the user signs into our app. This brings up the concept of *"Lifting"* state up to a *Parent* component so that the login state can be passed down as a *prop* to other components that will share this attribute later. Application state can only be passed down from Parent to Child component. As the complexity of the application grows, state management should be a top priority so that you can architect your UI accordingly. 

Our `src/App.js` file is what we will use as the Parent component for our application to manage a simple authentication scheme; and we will pass down the authentication state of the app as a `prop` to the remaining Child components that we will implement to deliver the functionality of our wallet. We will create a `handler` function that will allow us to determine if a user is authenticated by setting the user's authentication state in our Parent component or the `src/App.js` file that we are using to render our application's UI components.

Using a flag to determine the user's authentication state will allow us to implement a function to change the state of the flag every time a user signs into, or out of our application. To initialize our flag that we are using as a state attribute with the function that we will create to update the state changes we need to account for when our users login or out, we will need to pass a reference to this function to the `<Signin />` component that will use it to update the state attribute in `src/App.js` on user login or logout.

### Implement Routes with Access to the App Session

With Amazon Cognito we can access the session state declared in our Parent component, and we can pass it into the Child component created by the application for each of our routes. Using the appropriate property attributes or `props` in our case, copy and paste the following object that you need to add into your `src/App.js` file just below your `render()` function to store the authentication state for each user that signs into our app.

```
	const childProps = {
	  isAuthenticated: this.state.isAuthenticated,
	  userHasAuthenticated: this.userHasAuthenticated
	};
```
Having declared an object that will hold the value of the authentication state that you need to pass into each rendered component used by your application, you now need to pass the object and its values into the `<Route />` component that is declared at the end of the `render()` function in your `src/App.js` file. The declaration of the route component should now look like this: `<Routes childProps={ childProps } />` and the entire updated `src/App.js` file needs to look like this:

```
/*
  myPay Wallet
  P2P anonymous payments
*/

import React, { Component } from 'react'; // Added Component
// Use Link (see r-r-d docs here), for ref to home without refresh
// Import navbar component given to you by bootstrap 
import { NavLink } from "react-router-dom";
import Navbar from "react-bootstrap/Navbar";
import Nav from "react-bootstrap/Nav";
import NavDropdown from "react-bootstrap/NavDropdown";
import Routes from "./Routes";
import './App.css';

// We need a component to "contain" our App
class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      isAuthenticated: false
    };
  }

  userHasAuthenticated = authenticated => {
    this.setState({
      isAuthenticated: authenticated
    });
  }

  // Need to render App container
  render() {

    const childProps = {
      isAuthenticated: this.state.isAuthenticated,
      userHasAuthenticated: this.userHasAuthenticated
    };

    return (
      // should probably discuss className syntax in article
      <div className="App container">
        <Navbar bg="light" expand="lg">
          <Navbar.Brand as={ NavLink } to="/">
            MyPay Wallet
          </Navbar.Brand>
          <Navbar.Toggle aria-controls="basic-navbar-nav" />
          <Navbar.Collapse id="basic-navbar-nav">
            <Nav className="navigate">
              <Nav.Link as={ NavLink }
                to="/register"
                className="navi-link"
                exact>
                Register
              </Nav.Link>
              <Nav.Link as={ NavLink }
                to="/login"
                className="navi-link"
                exact>
                Login
              </Nav.Link>
            </Nav>
          </Navbar.Collapse>
        </Navbar>
        <Routes childProps={ childProps } />
      </div>
      );
  }
}
export default App;

```

The fact is we still have plenty of work to get our application to actually do something we these values now. Our routing mechanism with `react-router` has to initialize the Child component that the user requests with these `props`, and in our first use-case we will use them with our `Signin` component so that we can set our application's initial authentication state, just to get this thing finally working!

#### Project Structure and HOC's

Let's take a moment to talk about an advanced technique used in React.js as an emergent design pattern, because of its ability to allow developers to implement composite functions. Yes a function as an input to another function, or in the case of *Higher Order Components* in React.js, **a function that accepts a Component as an argument to return a new Component** that we can leverage to reuse Component logic. We need to use this concept to implement an *HOC* that will create a new `Route` for us that renders a new Child Component that will have the property values that have to be stored for use in the UI to deal with the appropriate state changes triggered by our users.

Ideally we should define an algorithm to follow for the implementation of our use case and its *HOC* that we will use to give us the Child component we need with all of the properties we are going to use to trigger an optimal user experience. The tool we are designing should be able to execute the following series of actions:

1. The *HOC* will output s new `<Route />` component that will include all of the properties neded by the child component rendered by the app. We will use a property, `component` to render the appropriate route that is found by its reference to the component that we want shown in the UI. The `childProps` object we declared in `src/App.js` will be passed into the component that we output from our *HOC*.

2. We will also create a render method that we can pass into the `Route` component that will output from our *HOC* instead of a component, to better control what we pass into our route components. Our *HOC* will return a `Route` by accepting both a component and `childProps` as `props` inputs to enable us to provide the component and the property values that have to be rendered to the UI.

3. We will declare an object that will will pass into our function that will define the values of our `component` as `C` and the properties that we want to set and render inside of our `Route` as `cProps`. We will pass a render function also that will output the new component we desire.

Below is the implementation of the *HOC* that we defined above:

```
import React from "react";
import { Route } from "react-router-dom";

export default ({
	component: C,
	props: cProps,
	...rest
}) => <Route
		{ ...rest }
		render={
			props => <C { ...props } { ...cProps } />
		}
	  />;
```

Since we will use this implementation to dynamically provide us with the routes and properties that we need for each component that we will render to our user, we will also need to refactor our existing `src/Routes.js` file so that we can use the new `childProp` values that we are passing into each of the new components that our new `Route` component will output to the UI.


























