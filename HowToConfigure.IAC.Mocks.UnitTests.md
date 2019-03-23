# Part 3 : How To Configure Infrastructure As Code, Mock Services, & Unit Testing 

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

*Publisher: [UniqueSoftwareDevelopment](https://www.uniquesoftwaredev.com)*

This is a continuation of our multi-part series on building a simple web application on [AWS]() using [AWS Lambda]() and the [ServerlessFramework](). You can review the first and second parts of this series starting with the setup of your `local` environment at:

* [Part 1: How To SetUp Your `local` Serverless Environment](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToSetUpYourLocalServerlessEnvironment.md)

* [Part 2: How To Configure Your Serverless Backend API](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md)

You can also clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer to this repo as you follow along with this tutorial.

## Configuring Infrastructure As Code

The [ServerlessFramework]() lets you describe the infrastructure that you want configured for your serverless + microservice based application logic. You can use template files in `.yml` or `.json` format to tell [AWS CloudFormation]() what exact resources you need deployed on [AWS]() to correctly run your application. The `YAML` or `JSON`-formatted files are literally the blueprints you design and architect to build your services with [AWS]() resources. We can see that in using the [AWS Template Anatomy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html) to describe our infrastructure, that the templates on [AWS CloudFormation]() will include a few major sections described in the template fragments shown below:

**YAML-formatted**

This is a `YAML`-formatted template fragment. You can find more information on `JSON`-formatted templates at: [AWS Template Anatomy](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-anatomy.html).

```
---
AWSTemplateFormatVersion : "version date",

Description:
	String

Metadata:
	template metadata

Parameters:
	set of parameters

Mappings:
	set of mappings

Conditions:
	set of conditions

Transform:
	set of transforms

Resources:
	set of resources

Outputs:
	set of outputs
```

The `Resources` section of the template is the only section that is required in your `YAML` or `JSON`-formatted template. When describing the services you need deployed to [AWS]() on your [CloudFormation]() templates it will be helpful to use the order I will be describing below because some sections may refer to values in a previous section, however, you can include these sections in your template in any order that you feel is appropriate. 

1. **Format Version (optional)**

	* This is the [AWS CloudFormation]() template version that the `YAML` or `JSON`-formatted file abides by. This is an versioning format internal to [AWS]() and can change independently of any API or WSDL versions published.

2. **Description (optional)**

	* This is simply a description of the template on [AWS CloudFormation](). If used, this section must always be included after the **Format Version** section listed above. 

3. **Metadata (optional)**

	* You can use this object to give [CloudFormation]() more information about the application and the template you are using to use [AWS]() infrastructure. 

4. **Parameters (optional)**

	* These are values that you can declare and pass to your `serverless.yml` file at runtime when you update or create a stack on [CloudFormation](). You can use these paramters and call them from the `Resources` or `Outputs` sections defined in your `serverless.yml` file.

5. **Mappings (optional)**

	* If you are familiar with *lookup tables*, you will find that you can use this section to specify conditional parameters with a mapping of associated *key:value* pairs. You can easily match *key:value* pairs with an [**Fn::FindInMap**](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/intrinsic-function-reference-findinmap.html) function within the `Resources` and `Outputs` sections.

6. **Conditions (optional)**

	* You can also control whether certain resources are created or if your resource properties are assigned the values that you declare when a stack is updated or created in [AWS](). Depending on whether or not a stack is for a development or production environment, you can for example, conditionally create a resource for each stage as needed by your application. 

7. **Transform (optional)**

	* With [**AWS::Include**]() you can use `transform` to work with `serverless.yml` [*gists*](https://stackoverflow.com/questions/6767518/what-is-the-difference-between-github-and-gist) that may be stored in a separate directory from your main `serverless.yml` template file. You can save your [*gists*](https://stackoverflow.com/questions/6767518/what-is-the-difference-between-github-and-gist) in an [Amaxon S3 bucket]() to reuse your functions across an infinite amount of `serverless.yml` files. You can also use this to better define your [AWS Serverless Application Model (AWS SAM)](https://github.com/awslabs/serverless-application-specification) files. However, because we are using the [ServerlessFramework]() we will not discuss how to use `transform` with [AWS SAM](https://github.com/awslabs/serverless-application-specification) here.

8. **Resources (REQUIRED)**

	* This is the only required *Template Section* that **MUST** be included in your `serverless.yml` file in your serverless backend. You **SHALL** use this section to specify the precise stack resources and their properties that you need [AWS CloudFormation]() to create for you on [AWS](). You can use [ServerlessFramework to define the infrastructure you need](https://serverless.com/framework/docs/providers/aws/guide/resources) to deploy with your `serverless.yml` file.

9. **Outputs (optional)**

	* This section will let you view your properties on the [CloudFormation]() stack and the values that it returns to you. You can easily use the [AWS CLI]() to use commands that will display the values returned by your stack for outputs that are declared in your `serverless.yml` file.

In our [CloudFormation Template]() called `serverless.yml` found in each our serverless + microservices that  we implement for our API, we describe the [AWS Lambda]() functions, [API Gateway]() endpoints to configure, [DynamoDB tables](), [Cognito]() User & Identity Pools, and [S3 Buckets]() that we need to deploy our serverless + microservice properly. This reality is what we call **Infrastructure As Code**. The goal in using and **IAC Architecture** is to reduce or prevent errors by avoiding the [AWS Management Console](). When we describe our **Infrastructure As Code** we can quickly and easily create multiple environments with minimal development time and effort exerted.

Transpiling and converting [**ES Code**]() to [Node v8.10]() is taken care of by the [serverless-webpack]() plugin that is included with the [ServerlessFramework]().

### AWS Resources & Property Types Reference

This is the [AWS Resource & Property Types Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) information for the resources and properties that [AWS CloudFormation]() supports as *Infrastructure As Code*. Resource type identifiers **SHALL** always look like this:

`service-provider::service-name::data-type-name`

We will use a few of the services that you can find at the [AWS Resource & Property Types Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html). Below you will find a list of the resources in our demo application that we have implemented for this tutorial:

* **[API Gateway]()**
* **[CloudFormation]()**
* **[DynamoDB]()**
* **[Lambda]()**
* **[S3]()**

For now, please open the `serverless.yml` file located at the [**ServerlessStarterService**](https://github.com/lopezdp/ServerlessStarterService) repository. Please take a look at the sections below for an explaination of each declaration in our [ServerlessFramework]() [CloudFormation]() template:

```
# TODO: https://serverless.com/framework/docs/providers/aws/guide/intro/

# New service names create new projects in aws once deployed
service: serverless-starter-service(node.js)

# Use the serverless-webpack plugin to transpile ES6
# Using offline to mock & test locally
# Use warmup to prevent Cold Starts
plugins:
  - serverless-webpack
  - serverless-offline
  - serverless-plugin-warmup

# configure plugins declared above
custom:
  # Stages are based on what is passed into the CLI when running
  # serverless commands. Or fallback to settings in provider section.
  stage: ${opt:stage, self:provider.stage}

  # Load webpack config
  # Enable auto-packing of external modules
  webpack: 
    webpackConfig: ./webpack.config.js
    includeModules: true

  # ServerlessWarmup Configuration
  # See configuration Options at:
  # https://github.com/FidelLimited/serverless-plugin-warmup
  warmup:
    enabled: true # defaults to false
    forlderName: '_warmup' # Name of folder generated for warmup
    memorySize: 256
    events:
      # Run WarmUp every 720 minutes
      - schedule: rate(720 minutes)
    timeout: 20

  # Load secret environment variables based on the current stage
  # Fallback to default if it is not in PROD
  environment: ${file(env.yml):${self:custom.stage}, file(env.yml):default}

provider:
  name: aws
  runtime: nodejs8.10
  stage: dev
  region: us-east-1

  # Environment variables made available through process.env
  environment:
    #### EXAMPLES
    # tableName: ${self:custom.tableName}
    # stripePrivateKey: ${self:custom.environment.stripePrivatekey}
```

Taking a closer look at the `YAML`-formatted template above, the `service` block is where you will need to declare the name of your *serverless + microservice* with [CloudFormation](). The [ServerlessFramework]() will use this as the name of the stack to create on [AWS](). If you change this name and redeploy it to [AWS](), then [CloudFormation]() will simply create a new project for you in your [AWS]() account.

The `environment` block is where we load secrets saved in our `env.yml` file. You have to remember that [AWS Lambda]() only gives you *4KB* of space for this file which should be more than enough for our needs. The important this to remember is to keep your logic modular and do not put all of you application secrets in one file. Use and `env.yml` file for each *serverless + microservice* that you implement. The secrets and custom variables that we load from our `env.yml` file are based on the stage that we are deploying to at any given point in the development lifecycle using `file(env.yml):${self:custom.stage}`. If your stage is not defined, then our application will fallback to load everything under the `default:` block with `file(env.yml):default`. The [ServerlessFramework]() will check if `custom.stage` is available before falling back to `default`.

As shown in the example, we can also use this mechanism to add other custom variables that we may need loaded at any given time. Any environment variables can be added to the `environment` block using something like: 

`${self:custom.environment.DECLARE_YOUR_VARIABLE}`

Any custom variable that we declare in the manner shown above is made available to our [Lambda]() function with something like this: 

`process.env.DECLARE_YOUR_VARIABLE`

### Configure An API Endpoint

In the [**ServerlessStarterService**](https://github.com/lopezdp/ServerlessStarterService) `serverless.yml` [AWS CloudFormation]() template that describes our infrastructure, we define the functions that we have implemented as [Lambdas]() that we want exposed on [AWS](). You must remember that each *serverless + microservice* will have its own `serverless.yml` template in the project's `root` directory that will define the *endpoints* associated with each **serverless + microservice**. Below is an example of a [Lambda]() function defined in our [**ServerlessStarterService**](https://github.com/lopezdp/ServerlessStarterService) [CloudFormation]() template:

```
functions:
  # Defines an HTTP API endpoint that calls the microServerless function in handler.js
  # - path: url path is /microServerless
  # - method: GET request
  # - cors: enabled CORS (Cross-Origin Resource Sharing) for browser cross
  #     domain api call
  # - authorizer: authenticate using an AWS IAM Role
  displayService:
    handler: handler.starterService
    events:
      - http:
          path: starterService
          method: get
          cors: true
          authorizer: aws_iam
    # Warmup can be applied to each lambda to override 
    # settings in custom.warmup block globally.
    warmup:
      enabled: true
```

Do not think this information has to be memorized. *Use the Force* and read the *documentation* and as questions on [StackOverFlow]() to discuss with the larger community of *Jedi*. As needed don't forget to refer to the [AWS Resource & Property Types Reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html) information for the resources and properties that [AWS CloudFormation]() supports as *Infrastructure As Code*.

#### Your new serverless + microservice is now configured using the Infrastructure As Code architecture.

## Mocking Serverless + MicroServices before Deploying to AWS

We have to **mock**, or *fake* the input paramaters for a specific event needed by our [Lambda's]() with a `*.json` file to be stored in a directory within the *serverless + microservice* project that we will use by executing the [ServerlessFramework]()'s `invoke` command. The `invoke` [command will run your serverless + microservice code locally by emulating the AWS Lambda environment](). As the old saying goes however:

> "If everything was candy and nuts, everyday would be Christmas..." - unknown

You just have to remember that this is not a 100% perfect emulation of the [AWS Lambda]() environment. There will be some differences between your cloud environment and your `local` machine, but this will do for the vast majority of use-cases. There are a lot of discussions online, and tools available that promote different approaches that you can take to optimize your `local` environment and your machine for `local` development outside of the *Cloud*. We will be mocking the `context` of our *serverless + microservices* within this tutorial with simple mock data only. The study of these tools will be left for a futurute tutorial. We do however find resources like [LocalStack](https://github.com/localstack/localstack), which is a tool that provides an easy testing and mocking framework for developing Cloud applications on the [AWS Cloud](), very interesting, to say the least. Please feel free to experiment with [LocalStack](https://github.com/localstack/localstack) and let us know how it works, in the future we will extend this tutorial to include a guid on its implementation also.

When saving a `*.json`-formatted event in a `/<microservice-project-directory>/mocks` directory that we will use with the [ServerlessFramework]() `invoke` command we would invoke the local serverless `event` as shown below:

**Example Usage of `invoke`**

`$ serverless invoke local --function functionName --path mocks/testFile.json`

### `invoke` Options on `local`

* `--function` or `-f`: The name of the function in your microservice that you want to invoke locally. **Required**.

* `--path` or `-p`: The path to a `json` file storing the input data that needs to be passed to the invoked [Lambda]() as the envent in the queue. This path is relative to the `root` directory of the microservice.

* `--data` or `-d`: This is the `String` data you need to pass as an `event` to your [Lambda]() function. Be aware that if you pass both `--path` and `--data`, the information included in the `--path` file will overwrite the data that you passed with the `--data` flag.

* `--raw`: This flag will allow you to pass data as a *raw string*, even if the string you are working with is a `.json`-formatted string. If you do not set this flag, then any `.json`-formatted data that you pass into the CLI when you `invoke` on local will be parsed and passed to your function as an `object`.

* `--contextPath` or `-x`: This is the path to the `.json`-formatted file that you have to store the input `context` that will be passed to the function that you decide to `invoke` locally. This path is relative to the `root` directory of your *serverless + microservice*.

* `--context` or `-c`: This is `string` data that you want to pass as the `context` to the function that you want to `invoke` locally. The information included with the `--contextPath` flag will overwrite the data that you passed with the `--context` flag.

* `--env` or `--e`: This is a `string` that will represent an environment variable that you want to declare when you `invoke` your function locally. The format of the environment variable **SHALL** be defined with the following syntax: `<name> = <value>`. This can be reused for more that one environment variable that you may need declared in your application.






## Serverless Unit Testing & Code Coverage
















