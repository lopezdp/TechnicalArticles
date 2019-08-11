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

Let's take a moment to talk about an advanced technique used in React.js as an emergent design pattern, because of its ability to allow developers to implement composite functions. Yes a function as an input to another function, or in the case of *Higher Order Components* in React.js, **a function that accepts a Component as an argument to return a new Component** that we canleverage to reuse Component logic. We need to use this concept to implement an *HOC* that will create a new `Route`  for us that renders a new Child Component that will have the property values that have to be stored for use in the UI to deal with the appropriate state changes triggered by our users.

Ideally we should define an algorithm to follow for the implementation of our use case and its *HOC* that we will use to give us the Child component we need with all of the properties we are going to use to trigger an optimal user experience. The tool we are designing should be able to execute the following series of actions:

1. The *HOC* will output a new `<Route />` component that will include all of the properties neded by the child component rendered by the app. We will use a property, `component` to render the appropriate route that is found by its reference to the component that we want shown in the UI. The `childProps` object we declared in `src/App.js` will be passed into the component that we output from our *HOC*.

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

The file for the code above should be organized in a new directory that we will call `src/components` to help us maintain a separation of concerns between React.js component that we will use to make asynchronous calls to our serverless + microservices and the code that we write to render a beautiful UI. Save the file above as `src/components/AppliedRoute.js` and let's move on so I can show you how this thing works.

Since we will use this implementation to dynamically provide us with the routes and properties that we need for each component that we will render to our user, we will also need to refactor our existing `src/Routes.js` file so that we can use the new `childProp` values that we are passing into each of the new components that our new `Route` component will output to the UI.

Your new `src/Routes.js` file has to look like the source code you see here:

```
/*
  Pay Me Now Wallet
  P2P anonymous payments
  Routes.js
*/

import React from "react";
import { Route, Switch } from "react-router-dom";
import Home from "./containers/Home";
import Signin from "./containers/Signin";
import Page404 from "./containers/404Page";
import AppliedRoute from "./components/AppliedRoute";

export default ({childProps}) => <Switch>
                                   { /* This is our home page route for the main landing page tyo the app */ }
                                   <AppliedRoute path="/"
                                     exact
                                     component={ Home }
                                     props={ childProps } />
                                   { /* This is the Login Route */ }
                                   <AppliedRoute path="/login"
                                     exact
                                     component={ Signin }
                                     props={ childProps } />
                                   { /* This route will catch all unmatched routes && MUST BE LAST!!! */ }
                                   <Route component={ Page404 } />
                                 </Switch>
```                                 

Now we are using an `AppliedRoute` component everywhere that you need to set a series of `childProps` that we will use in our Child component, in our case we are accessing the `userHasAuthenticated` prop that manages the authentication state of our application from the `src/App.js` Parent component. To change the appliation state in our Parent component `src/App.js`, we have to trigger the `userHasAuthenticated(bool)` function that we declared in `src/App.js` that we passed into our `AppliedRoute` as a `childProp`.

In our `Signin` component our users will interact with the functionality that will log them into and out of our application. Inside of `/src/containers/Signin.js`, we need to make sure we have implemented the following line of code: `this.props.userHasAuthenticated(true)`.

This line of code has to executed after the call to signin with Cognito is made with: `await Auth.signIn(this.state.email, this.state.password);` inside of your `handleSubmit()` funtion that we will trigger when the login form is submitted by the user.

Your new `handleSubmit()` `async` function inside of your `src/containers/Signin.js` component should now look like this:

```
  // Use async promise to wait for response from aws-amplify api
  handleSubmit = async event => {
    event.preventDefault();

    // Amplify Authentication logic
    try {
      // Make call to Auth API using aws-amplify
      await Auth.signIn(this.state.email, this.state.password);
      this.props.userHasAuthenticated(true)
    } catch ( err ) {
      alert(err.message);
    }
  }
```

To execute this functionality we now have to implement a UI element that will let the user fire off these events. We need a sign out button and we need one quick.

#### Using a Button Element to Sign Off

We are now ready to start adding a few more interactive UI elements into the layout of the app. We need to apply the authenticate state functionality so that we can let our users interact with our app on Sign Out. When a user is authenticated, they will need to see a button that will let them sign out of our application also. We will accomplish this in React.js using a `<Fragment>` component. A `Fragment` is great for creating groups of child elements without cluttering the DOM full of extra nodes.

In our case we need an option to display two links in the UI when a user is not authenticated; we should display a *Register* and a *Sign In* link. In the case of an authenticated user, we need to only display a *Sign Off* link in the UI. We will accomplish this using a ternary operator and a `Fragment` component. When `this.state.isAuthenticated` is `true`, we will display the `Sign Off` link to the user. When the `isAuthenticated` flag is `flase` out ternary operator will return our new `Fragment` component where we will use `JSX` to declare our `Register` and `Sign In` links to the user. 

Make sure that the `source code` in your `src/App.js` file looks like the following file, while making sure to add `Fragment` to your list of `react` imports as shown below:

```
/*
  myPay Wallet
  P2P anonymous payments
*/

import React, { Component, Fragment } from 'react'; // Added Component
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

  // Update authentication state on signout event
  handleSignOut = async event => {
    this.userHasAuthenticated(false);
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
            { this.state.isAuthenticated
              ? <NavDropdown.Item onClick={ this.handleSignOut } className="navi-link">
                  Sign Out
                </NavDropdown.Item>
              : <Fragment>
                  { /* Fragment is like placeholder component */ }
                  <Nav.Link as={ NavLink }
                    to="/register"
                    className="navi-link"
                    exact>
                    Register
                  </Nav.Link>
                  <Nav.Link as={ NavLink }
                    to="/signin"
                    className="navi-link"
                    exact>
                    Login
                  </Nav.Link>
                </Fragment> }
          </Navbar.Collapse>
        </Navbar>
        <Routes childProps={ childProps } />
      </div>
      );
  }
}
export default App;
```

Take a look at the new `handleSignOut` `async` function that we defined above too. When called by the UI after the user triggers the `Sign Out` event, our application will call `handleSignOut` and change the `userHsAuthenticated` flag to `false` so that our application's authentication state can be updted to reflect the current state of the user's session as needed. See the code below for a better look at the function in question:

```
// Update authentication state on signout event
handleSignOut = async event => {
  this.userHasAuthenticated(false);
}
```

To check the implementation we have just worked through, we will need to create a user for ourselves from the command line or `terminal` since we dont have a mechanism to register a user with at the moment. Luckily for us, Amazon Cognito gives us a really easy way to do this using the following commands to create a user in Cognito that we can use to test our connections with.

##### Creating a Test User

Using an email address and a password we will run a few commands using the `AWS-CLI` that we installed in a previous chapter in this series. This user will also have to be confirmed so this will take few steps to complete. Below is the first command that you need to run from that `terminal` on your pretty `Mac Book Pro`.

```
$  aws cognito-idp sign-up \
   --region us-east-1 \
   --client-id 52sdl6jc2kk571gk2do3r39lol \
   --username davidplopez@live.com \
   --password Passw0rd!
```

Just like you did in your own `config.js` file, here you will need to do the same and use your own `client-id` and `region` values based on the *Service Information* and *Stack Outputs* you received when you deployed your service on CodePipeline in the previous chapter on CI/CD. Furthermore, before we can use this username to authenticate ourselves within our application, we will need to verify this user in Cognito with the fopllowing command:

```
$  aws cognito-idp admin-confirm-sign-up \
   --region us-east-1 \
   --user-pool-id us-east-1_IJ3kOWibj \
   --username davidplopez@live.com 
```

With this step complete we can now test our `Fragment` component to see if our `Sign Out` link is displayed to our users when they authenticate themselves against Cognito.

The following image is what you should be able to see on your own `local` environment:

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/SignOutLink.png "User Sign Off Link!")
































