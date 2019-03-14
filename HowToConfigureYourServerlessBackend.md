# Part 2: How To Configure your Serverless Backend on AWS

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first part of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

You can clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer to this repo as you follow along with this tutorial.

## Serverless Computing Architecture

Serverless programming and computing, or *serverless* for short, is a software architecture that enables an execution paradigm where the cloud service provider (AWS, GoogleCloud, Azure) is the entity responsible for running a piece of backend logic that you write in the form of a stateless function. In our case we are using [AWS Lambda](). The cloud provider you choose to run your stateless function, is responsible for the execution of your code in the cloud, and will dynamically allocate the resources needed to run your backend logic, by abstracting the deployment infrastructure for you, so that you can focus on developing your product instead of auto-scaling servers. This paradigm is sometimes refered to as *Functions As A Service or (FAAS)*. Your code will run inside of *stateless containers* that may be triggered by a number of events that can include: *cron jobs, http requests, queuing services, database events, alerts, file uploads, etc.*

### Serverless Considerations

Since the *serverless* paradigm abstracts away the need for an engineer to configure the underlying physical infrastructure typical to the deployment of a modern day application, in what is known as the new *Functions As A Service (FAAS)* reality, the following are a few considerations that should be kept in mind while we proceed through the development of our *Single Page Application*:

#### Microservices

When developing a *serverless* application, we need to make sure that the application is structured in a way in which the functions we declare as part of the backend logic, are defined in the form of individual services that mimic a *microservice* based architecture so that we may better be able to reduce the size of our functions. The goal is to *loosely couple* the functionality between the services deployed as a part of the serverless backend, so that each function is responsible for an independent piece of functionality that will provide a user with a response that does not rely on any other service. 

#### Stateless Functions

When we deploy a **serverless + microservice** architecture, the functions that we declare as a part of our application API, are executed inside of stateless containers for us by our cloud service provider, or in our case [AWS](). The significance of this is that our code is not run as it typically would be on a *server* that executes long after the event has completed. There is no prior execution context to serve a request to the users of your application when running [AWS Lambda](). Throughout the development of your serverless applications you MUST assume that your function is invoked in its initial application state every time, and with no contextual data to work with, because your function will not be handling concurrent requests. Your backend is stateless and each function should strive to return an *idempotent* response.

#### Cold Starts

Because our functions are executed inside of a stateless container that is managed by the cloud service provider, in our case [AWS](), there is a bit of latency associated with each `http request` to our serverless "backend". Our stateless infrastructure is dynamically allocated to respond to the events triggered by our application, and although the container is typically kept "alive" for a short period of time upon the completion of the [Lambda's]() functionality, the resources will be deallocated and will lead to slower than expected/desired responses for new requests. These are referred to as *Cold Starts*. 

*Cold Start* durations will typically last from a couple of hundred milliseconds to up to a few seconds. The size of the functions and the runtime language used can vary the *Cold Start* duration time in [AWS Lambda](). It is important to understand that our serverless containers *can* remain in an `Active` state in [AWS Lambda](), after the initial request to our serverless endpoint has completed its execution routine. If a subsequent request to our [Lambda]() is triggered by our application immediately after the completed execution of a previous request, the serverless lambda that defines our endpoint in the cloud in our stateless containers on [AWS](), will respond to this next request almost immediately and with little to no latency; this is called a *Warm Start*, and this is what we want to maintain to keep our application running optimally.

The great thing about working with the [ServerlessFramework]() library is the robust community that contributes to its development and evolution as `Serverless` becomes more of a thing. Dynamically allocating resources programatically to deploy applications to the cloud just feels more practical from where I am sitting as an `engineer` *working quietly on the cyber front*. Take a second to bookmark this [List of plugins developed by the community for the ServerlessFramework](https://github.com/Jimdo/plugins-serverless). We are going to use the [serverless-plugin-warmup](https://github.com/FidelLimited/serverless-plugin-warmup) package on *NPM*, to make sure that our functions keep warm and purring like my dad's old 1967 Camaro. I personally had a thing for *Lane Meyer's* (John Cusak) '67 Camaro in the [1980's *Cult Classic* *Better Off Dead*](https://www.youtube.com/watch?v=jfatrAqd22c).

**I want my $2!**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/warmStartCamaro.jpg#center "I still want my $2!!!")

#### Optimize for Warm Starts

As discussed above, we will be keeping our [Lambda's]() warm during the hibernation season with [serverless-plugin-warmup](https://github.com/FidelLimited/serverless-plugin-warmup).  In this next section, we will walk you through each step of the installation of this plugin. Remember, you can also refer to the sample of the application we will be using in this tutorial to follow along, here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git). 

[ServerlessWarmup](https://github.com/FidelLimited/serverless-plugin-warmup) eliminates *Cold Start* latency by creating a [Lambda]() that is scheduled to invoke all of the services you select from your API, at a `time interval` of your choice, the default is set at 5-minutes. Thereby forcing your [Lambda's]() to stay warm. From within the root of you serverless project directory, continue to install [ServerlessWarmup](https://github.com/FidelLimited/serverless-plugin-warmup) as follows:

* **Run:** `$ npm install --save-dev serverless-plugin-warmup`

Add the following line to the `plugin` block in your `serverless.yml` file that is found in the root of your service's directory:

```
plugins:
	- serverless-plugin-warmup
```

Take a look at what my file looks like if you need a reference point:

**serverless.yml `plugin` block**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/serverless-warmup-blockYML.png#center "Serverless.yml Plugins!")


























