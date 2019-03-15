# Part 2: How To Configure your Serverless Backend on AWS

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first part of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

You can clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer to this repo as you follow along with this tutorial.

## The Serverless Architecture

Serverless programming and computing, or *serverless* for short, is a software architecture that enables an execution paradigm where the cloud service provider (AWS, GoogleCloud, Azure) is the entity responsible for running a piece of backend logic that you write in the form of a stateless function. In our case we are using [AWS Lambda](). The cloud provider you choose to run your stateless function, is responsible for the execution of your code in the cloud, and will dynamically allocate the resources needed to run your backend logic, by abstracting the deployment infrastructure for you, so that you can focus on developing your product instead of auto-scaling servers. This paradigm is also known to be called *Functions As A Service or (FAAS)*, and the code will run inside of *stateless containers* that may be triggered by a number of events that can include: *cron jobs, http requests, queuing services, database events, alerts, file uploads, etc.*

### Serverless Considerations

Since the *serverless* paradigm abstracts away the need for an engineer to configure the underlying physical infrastructure typical to the deployment of a modern day application, in what is known as the new *Functions As A Service (FAAS)* reality, the following are a few considerations that should be kept in mind while we proceed through the development of our *Single Page Application*:

#### Stateless Computing

When we deploy a **serverless + microservice** architecture, the functions that we declare as a part of our application API, execute our application’s logic inside of stateless containers for us by our cloud service provider, or in our case [AWS](). The significance of this is that our code does not run as it typically would be on a *server* that executes long after the event has completed. There is no prior execution context to serve a request to the users of your application when running [AWS Lambda](). Throughout the development of your serverless applications, you MUST assume that [AWS Lambda]() will invoke your function as if it is in its first application state every time, and with no contextual data to work with, because your function will not be handling concurrent requests. Your backend is stateless, and each function should strive to return an *idempotent* response.

#### Serverless + Microservices

When developing a *serverless* application, we need to make sure that the application is structured in a way in which the functions we declare as part of the backend logic, are defined in the form of individual services that mimic a *microservice* based architecture so that we may better be able to reduce the size of our functions. The goal is to *loosely couple* the functionality between the services deployed as a part of the serverless backend, so that each function handles an independent piece of functionality that will provide a user with a response that does not rely on any other service.

#### Cold Starts

Because our functions execute inside of a stateless container that our cloud service provider manages for us, in our case [AWS](), there is a bit of latency associated with each `http request` to our serverless "backend". Our stateless infrastructure is dynamically allocated to respond to the events triggered by our application, and although the container is typically kept "alive" for a short time after completion of the [Lambda's]() functionality, the resources will be deallocated and will lead to slower than expected/desired responses for new requests. We refer to these situations as *Cold Starts*.

*Cold Start* durations will typically last from a couple of hundred milliseconds to up to a few seconds. The size of the functions and the runtime language used can vary the *Cold Start* duration time in [AWS Lambda](). It is important to understand that our serverless containers *can* remain in an `Active` state in [AWS Lambda](), after the first request to our serverless endpoint has completed its execution routine. If a subsequent request to our [Lambda]() is triggered by our application immediately after the completed execution of a previous request, the serverless lambda that defines our endpoint in the cloud in our stateless containers on [AWS](), will respond to this next request almost immediately and with little to no latency; this is called a *Warm Start*, and this is what we want to maintain to keep our application running optimally.

The wonderful thing about working with the [ServerlessFramework]() library is the robust community that contributes to its development and evolution as `Serverless` becomes more of a thing. Dynamically distributing resources programmatically to deploy applications to the cloud just feels more practical from where I am sitting as an `engineer` *working quietly on the cyber front*. Take a second to bookmark this [List of plugins developed by the community for the ServerlessFramework](https://github.com/Jimdo/plugins-serverless). We are going to use the [serverless-plugin-warmup](https://github.com/FidelLimited/serverless-plugin-warmup) package on *NPM*, to make sure that our functions keep warm and purring like my dad's old 1967 Camaro. I personally had a thing for *Lane Meyer's* (John Cusack) '67 Camaro in the [1980's *Cult Classic* *Better Off Dead*](https://www.youtube.com/watch?v=jfatrAqd22c).

**I want my $2!**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/warmStartCamaro.jpg#center "I still want my $2!!!")

#### Configure AWS Lambda & Decrease your Application’s Latency with Warm Starts

As discussed above, we will be keeping our [Lambda's]() warm during the hibernation season with [serverless-plugin-warmup](https://github.com/FidelLimited/serverless-plugin-warmup). In this next section, we will walk you through each step of the installation of this plugin. Remember, you can also refer to the sample of the application we will be using in this tutorial to follow along, here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git).

[ServerlessWarmup](https://github.com/FidelLimited/serverless-plugin-warmup) eliminates *Cold Start* latency by creating a [Lambda]() that will schedule and invoke all the services you select from your API, at a `time interval` of your choice, the default is set at 5-minutes. Thereby forcing your [Lambda's]() to stay warm. From within the root of you serverless project directory, continue to install [ServerlessWarmup](https://github.com/FidelLimited/serverless-plugin-warmup) as follows:

* **Run:** `$ npm install --save-dev serverless-plugin-warmup`

Add the following line to the `plugin` block in your `serverless.yml` file that you can find in the root of your service's directory:

```
plugins:
  - serverless-plugin-warmup
```

Look at what my file looks like if you need a reference point:

**serverless.yml `plugin` block**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/serverless-warmup-blockYML.png#center "Serverless.yml Plugins!")

Moving along now, you will want to configure the `serverless-warmup-plugin` in the `custom:` block of your service's `serverless.yml` file. Remember, each service will always have its own `serverless.yml` file that will define the [AWS Lambda]() endpoints for each **serverless + microservice** implemented for each path defined in the `functions:` block of the file. There are a few configuration settings you can read more about at the `serverless-warmup` [Documentation repository](https://github.com/FidelLimited/serverless-plugin-warmup). Here we will go over what we think are the most important settings you should at least be familiar with for now. Your `custom:` block in your `serverless.yml` file should look something like this:

```
custom:
  # Stages are based on what we pass into the CLI when running
  # serverless commands. Or fallback to settings in provider section.
  stage: ${opt:stage, self:provider.stage}

  # Load webpack config
  webpack:
    webpackConfig: ./webpack.config.js
    includeModules: true

  # ServerlessWarmup Configuration
  # See configuration Options at:
  # https://github.com/FidelLimited/serverless-plugin-warmup
  warmup:
    enabled: true # defaults to false
    folderName: '_warmup' # Name of folder generated for warmup
    memorySize: 256
    events:
      # Run WarmUp every 60 minutes Mon-Fri between 8:00am and 5:55pm (UTC)
      - schedule: rate(60 minutes)
    timeout: 20
```

If you are being perceptive right now, you will notice that this `serverless.yml` file is really letting us complete a lot of interesting tasks quickly, and without having to think too much about the impact of the resources we are conjuring-up out of thin air. As you can see *Young Padawan*, we are slowly, but surely making our way through a concept known as **Infrastructure As Code**, and we are, albeit moderately for now, programmatically allocating and *spinning-up* the cloud-based servers we need to keep our [Lambda's]() warm with this [serverless-warmup-plugin](https://github.com/FidelLimited/serverless-plugin-warmup).

We will get back to **Infrastructure As Code** in a bit, but this idea of *serverless...servers*??

**Irony in the Cloud**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/cloud-servers.png#center "Serverless Servers...")

### Understanding [AWS Lambda]()

We really must discuss how [AWS Lambda]() will execute the logic within our functions to better understand, and to have a general idea about a few of the important properties that make up our [AWS FaaS]() paradigm. Below are a few details you should know about how [Lambda]() works with you:

**[AWS Lambda]() Specs**
Lambda will support the runtime environments listed below:
* **Node.js:** v8.10 & v6.10
* **Java 8**
* **Python v3.6 & v2.7**
* **.NET Core: v1.0.1 & v2.0**
* **Go v1.x**
* **Ruby v2.5**
* **Rust**

Each [Lambda]() will execute and compute inside of a container with a 64-bit AWS Linux AMI. [AWS]() will distribute our [Lambda’s]() computational needs to each user according to the following system requirements:
* **Memory:** 128MB - 3008MB (Allocated in 64MB increments)
* **Ephemeral Disk Space:** 512 MB
* **Max execution time:** 900 seconds
* **Uncompressed Package Size:** 250 MB
* **Compressed Package Size:** 50MB

The `serverless` design paradigm is a language agnostic approach that is meant to give engineers the ability to leverage [AWS]() resources and infrastructure to better scale their products, i.e. your products, to a global market place and to more quickly put your innovation into the hands of the users that need it the most.

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AWSLambdaFunction.png#center "This is an AWS Lambda Function!!!")























