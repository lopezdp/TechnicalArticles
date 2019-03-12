# Part 2: How To Configure your Serverless Backend on AWS

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first part of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

## Serverless Computing Architecture

Serverless programming and computing, or *serverless* for short, is a software architecture that enables an execution paradigm where the cloud service provider (AWS, GoogleCloud, Azure) is the entity responsible for running a piece of backend logic that you write in the form of a stateless function. In our case we are using [AWS Lambda](). The cloud provider you choose to run your stateless function, is responsible for the execution of your code in the cloud, and will dynamically allocate the resources needed to run your backend logic, by abstracting the deployment infrastructure for you, so that you can focus on developing your product instead of auto-scaling servers. This paradigm is sometimes refered to as *Functions As A Service or (FAAS)*. Your code will run inside of *stateless containers* that may be triggered by a number of events that can include: *cron jobs, http requests, queuing services, database events, alerts, file uploads, etc.*

### Serverless Considerations

Since the *serverless* paradigm abstracts away the need for an engineer to configure the underlying physical infrastructure typical to the deployment of a modern day application, in what is known as the new *Functions As A Service (FAAS)* reality, the following are a few considerations that should be kept in mind while we proceed through the development of our *Single Page Application*:

#### Microservices

When developing a *serverless* application, we need to make sure that the application is structured in a way in which the functions we declare as part of the backend logic, are defined in the form of individual services that mimic a *microservice* based architecture so that we may better be able to reduce the size of our functions. The goal is to *loosely couple* the functionality between the services deployed as a part of the serverless backend, so that each function is responsible for an independent piece of functionality that will provide a user with a response that does not rely on any other service. 

#### Stateless Functions

When we deploy a **serverless + microservice** architecture, the functions that we declare as a part of our application API, are executed inside of stateless containers by the cloud service provider, or in our case [AWS](). The significance of this is that our code is not run as it typically would be on a *server* that executes long after the event has completed. There is no prior execution context to serve a request to the users of your application when running [AWS Lambda](). Throughout the development of your serverless applications you MUST assume that your function is invoked in its initial application state every time and with no contextual data to work with because your function will not be handling concurrent requests.

#### Cold Starts


