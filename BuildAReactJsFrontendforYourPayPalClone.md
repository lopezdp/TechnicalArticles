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

## Start a New React.js Project

Now that we have a bunch of fancy logic on our [AWS Cloud](), we need to develop a pretty user interface that we can use to attract real *humans* to our money trap, I mean... *Wallet*. Since the [Facebook Mafia]() is much smarter than us, we are just going to go ahead and use something called [Create React App, or `create-react-app` for those who are more programatically inclined](https://github.com/facebook/create-react-app).






