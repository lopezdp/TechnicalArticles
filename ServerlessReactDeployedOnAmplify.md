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



