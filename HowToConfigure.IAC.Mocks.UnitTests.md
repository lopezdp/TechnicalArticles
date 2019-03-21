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

The `Resources` section of the template is the only section that is required in your `YAML` or `JSON`-formatted template. When describing the services you need deployed to [AWS]() on your [CloudFormation]() templates it will be helpful to use the order I will be describing below because some sections may refer to values in a previous section, however, you can in fact include these section in your template in any order that you feel is appropriate.



## Mocking Serverless + MicroServices before Deploying to AWS

## Serverless Unit Testing & Code Coverage
















