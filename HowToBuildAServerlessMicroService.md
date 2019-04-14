# Part 5 : How To Build a Serverless + MicroService for your Application

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

You can [clone the invoice-log-api](https://github.com/lopezdp/invoice-log-api) that we are starting out with, but we think it is best if you just follow along with us through each step, so you can better internalize the lessons to be learned in this tutorial my young *padawan*. Let me know when you get sick of the *Star Wars* references and we  will double down a bit more. Let's do this:

We are going to continue on, where we left off in [Part 2 of Setting up your `local`](https://github.com/lopezdp/TechnicalArticles/blob/master/HowToConfigureYourServerlessBackend.md#setup-serverless-framework-locally) serverless environment. We walked through creating a `local` project structure that resembled something like this after you renamed your template:

```
    PayMyInvoice
    |__ services
       |__ invoice-log-api (renamed from template)
       |__ FutureServerlessMicroService (TBD)
```

Proceed to navigate into the `invoice-log-api` service where we will now implement a few [Lambda functions]() that we need to serve our **PayMyInvoice** application. The first thing a user of our application will need to do is to create an invoice that the user can send to someone who will receive it and make a payment to our system based on the amount of the invoice. After having initially implemented this service to be able to more effectively write this tutorial for you, I now realize that I have forgotten to add fields for `Payee` information and `email` which would really be helpful within the scope of this application! Either way, my mistake is your success! 

### Implement `createInvoice.js`

Here is what you will need to implement to be able to let your users create an invoice that they can use to accept payments for from a third-party within our new payment system. I have left a few comments within the source code to provide some insight on what each line of code is trying to achieve. We will review these in a bit of detail to be sure you are comfortable implementing a few [Lambda's]() in the future on your own!

**creatInvoice.js**

```
// Step1: Discuss the uuid import and need for uuid
import uuid from "uuid";
// Step2: Discuss in tutorial why /lib and responseLib
// exist and why they are used.
import { success, failure } from "./libs/responseLib";

// Step3: Discuss in tutorial the need for a Dynamo table
// and a dynamo table implemented for each microservice
// Implement service below
import * as dynamoLib from "./libs/dynamoLib";

export async function main(event, context) {
  // The request body is passed in as a JSON string
  // in event.body and it needs to be parsed!
  const data = JSON.parse(event.body);

  // Now you need to store the information into an
  // object that you will use later to store the data
  // collected from your user into a database of invoices!
  const params = {
    // Step4: Need to describe in tutorial how this object is
    // accessing the table defined in the serverless.yml
    // and how data is being stored in db.
    TableName: process.env.invoiceTbl,
    /*
     * 'Item': contains the ttributes of the item to create
     *         In NoSql this is equivalent to a row of data
     *
     *    - 'userID': user identities are federated through
     *                the CognitoIdentity Pool (MUST create),
     *                and we need to use an identityID as the
     *                userId of the Authenticated User.
     *
     *    - 'invoiceID': a uuid that is unique to this record
     *    - 'createdAt': this is the current UNIX timestamp
     *    - 'payerEmail': this is the email of the invoice Payer
     *    - 'description': this is the description of the
     *                     transaction as entered by the user
     *                     and parsed from the Request.body
     *
     *    - 'amount': this is the amount of the transaction
     *                as entered by the user and parsed from
     *                the Request.body also
     *
     *    - 'attachment': This any file the user may attach
     *                    to the record that the system will
     *                    store in an s3 bucket and parsed
     *                    from the request.body too
    */
    Item: {
      // Step5: Discussion on DynamoDB sort key design and
      // how to properly aggregate data in table to
      // minimize READS (RCU) from cloud to minimize cost!!!
      userId: event.requestContext.identity.cognitoIdentityId,
      invoiceId: uuid.v1(),
      createdAt: Date.now(),
      description: data.description,
      amount: data.amount,
      attachment: data.attachment

    }
  };

  try {
    // async call to db??????
    // need to implement and test!!!!
    // need a lib to make calls to aws dynamo
    // to persist data for new invoices created
    await dynamoLib.call("put", params);
    return success(params.Item);
  } catch ( err ) {
    return failure({
      status: false
    });
  }
}

```

We'll break this first one down by steps just to be sure this is all clear to you; *Step1* is where we import the functionality needed to allow us to generate a new `uuid` for each invoice created.








