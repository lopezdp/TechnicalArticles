# Part (****) : How To Build a Serverless + MicroService for your Application

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first and second parts of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

* [Part 2: How To Configure Your Serverless Backend API](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md)

* [Part 3: How To Configure Your Infrastructure As Code, Mock Services, & Unit Testing](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigure.IAC.Mocks.UnitTests.md)

* [Part 4: How To Deploy and Configure an effective CI/CD Pipeline on AWS](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToReviewServiceToConfigureCICDpipeline.md#part-4--code-review-deploy--configure-an-effective-cicd-pipeline-on-aws)

You can also clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer to this repo as you follow along with this tutorial.

## System Architecture & Project Structure

We will start by structuring our project directory according to what we will build today. I have done a lot of work in the *payments* industry, and I always enjoy looking for ways to make it easier to send or receive money between people. In my opinion, *sustainability* and *monetization* are synonymous. You cannot sustain any of your projects without [Cash Money](). We will build a *time-sheet* application that will allow a user to login to the demo application, create an invoice with a description of work, to send it to an email to notify a *third party* and accept payment for the invoice created. We will call this the **PayMeNow** application.

You can [clone the application](https://github.com/lopezdp/ServerlessStarterService.git) at the resource we have provided, but we think it is best if you just follow along with us through each step, so you can better internalize the lessons to be learned in this tutorial my young *padawan*. Let me know when you get sick of the *Star Wars* references and we  will double down a bit more. Let's do this:

Proceed to a directory on your machine where you want to get this project started and create a directory like:

`$ mkdir PayMeNow`









