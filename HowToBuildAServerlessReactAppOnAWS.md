# How To Build a Serverless React.js Application with AWS Lambda, API Gateway, & DynamoDB

*Author: [David P. Lopez](http://www.DavidPLopez.com)*

You can clone a sample of the application we will be using in this tutorial here: [Serverless-Starter-Service](https://github.com/lopezdp/ServerlessStarterService.git)

Please refer to this repo as you follow along with this tutorial.

### Introduction

It is amazing how quickly the technology community iterates over innovative technology frameworks, and architectural paradigms to solve the never-ending series of problems and *work-arounds* that a new tool, or *solution* inevitably brings to the table. Even more enjoyable to watch is the relentless chatter and online chat and commentary that spreads like wildfire all over the internet and the *Twittersphere*, that goes on discussing how to use the latest toolset and framework to build the next software that will **Change the World for the Better**. I must admit, although I sound cynical about the whole thing, I too am a part of the problem; I am an **AWS Serverless Fanboy**.

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/AWSServerless.png "AWS Serverless Architecture")

The aim of this tutorial is to deploy a simple application on [AWS]() to share with you, our favorite readers, the joys of developing applications on the [Serverless Framework]() with [AWS](). The application we will be walking you through today, includes a backend API service to handle basic **CRUD** operations built on something we like to call the **DARN Technology Stack**. Yes, we created a new acronym for your recruiter to get excited about. They will have no idea what you are talking about, but they will get you an interview if you tell them that you completed this tutorial to become a fully-fledged and certified *Application Developer on the DARN Cloud*. The **DARN Stack** includes the following tool set:

* **D**ynamoDB
* **A**WS Serverless Lambda
* **R**eact.js
* **N**ode.js

### Technology Stack

For a more precise list of tools that we will be implementing throughout the development lifecycle of this multi-part series, below I have highlighted the technologies that we will be using to deploy our application on AWS using the [ServerlessFramework]():

* [AWS Lambda]() & [API Gateway]() to expose the API endpoints
* [DynamoDB]() is our NoSQL database
* [Cognito]() supplies user authentication and secures our API's
* [S3]() will host our application & file uploads
* [CloudFront]() will serve our application to the world
* [Route53]() is our domain registry
* [Certificate Manager]() provides us with SSL/TLS certificates
* [React.js]() is our single page application
* [React Router]() to develop our application routing functionality
* [Bootstrap]() for the development of our UI components
* [Stripe]() will process our credit card payments
* [GitHub]() will our project repositories

### Local Development Environment Setup & Configuration

One of the more difficult activities I faced as a junior developer a very long, long, time ago was understanding that the type of project that I would be working on, very much dictated how I would eventually have to configure my machine *locally*, to be ready to develop *ground breaking and world changing software*. Anytime you read a mention to *world changing software* from here on out, please refer to episodes of **HBO's Silicon Valley** to understand the *thick sarcasm* sprinkled throughout this article. My point is that I have always felt that most tutorials seem to skim over the idea of setting up your *local development environment*, as if it were a given that developers were born with the inherent understanding of the differences between `npm`, `yarn`, `bower`, and the never ending list of package managers and slick tools available to 'help' you succeed at this life in `SoftwareDevelopment`... For a historical perspective with a wholistic take on this matter please brush up on your knowledge of a topic some people refer to as [RPM Hell](http://wiki.c2.com/?RpmHell).

To avoid [Dependency Hell](http://wiki.c2.com/?DependencyHell), we have decided to codify and create a series of *Best Practices* you can take with you for the development of the application in this tutorial and any other projects you work on in the future. For the goals of completing the application in this tutorial please make sure to configure all `local` development machines using the tools, dependencies, and configuration parameters described in this article. This list is not definitive and is only meant as a baseline from which to begin the development of your applications as quickly and as easily as possible.

#### JavaScript Toolkit

- [ ] Node Version Manager
- [ ] Editor
  * SublimeText3
    1. PackageControl
    2. Babel
    3. ESLint
    4. JSFMT
    5. SublimeLinter
    6. SublimeLinter-eslint (Connector)
    7. SublimeLinter-annotations
    8. Oceanic Next Color Scheme
    9. Fix Mac Path (Only If using MacOS)
- [ ] AWS CLI
- [ ] Serverless Compute
  * AWS Lambda
- [ ] Infrastructure As Code
  * [ServerlessFramework](https://serverless.com)
- [ ] Package Manager
  * `npm`
- [ ] Automation Approach
  * [npmScripts](https://docs.npmjs.com/misc/scripts)
- [ ] Transpiling
  * Babel ([Included in ServerlessFramework!](https://babeljs.io))
- [ ] Module Format
  * ES6Modules (CommonJS)
- [ ] Bundling
  * WebPack4 (Included in ServerlessFramework![serverless-webpack]](https://github.com/serverless-heaven/serverless-webpack))
- [ ] Linting
  * ESLint
  * eslint-plugin-react
  * babel-eslint
  * esformatter
  * esformatter-jsx
- [ ] Testing
  * [Jest](https://jestjs.io)
- [ ] Continuous Integration Server
  * AWS CodeDeploy & CodePipeline
- [ ] HTTP Mock Framework
  * [Included in ServerlessFramework!](https://serverless.com)
- [ ] Sourcemaps
  * [Babel: SourceMap Support NPM Plugin](https://www.npmjs.com/package/babel-plugin-source-map-support)

#### Install Node.js with NVM (Node Version Manager)

On 7 November 2018, [AWS]() announced to the world that [AWS Lambda](), will now officially support [Node.js v8.10.0](). This project will use [NVM (Node Version Manager)]() to work with different versions of [Node.js]() between projects and to mitigate against any potential environment upgrades implemented in the future by any 3rd party vendors. To ensure that we are working on the correct version of [Node.js]() for this project please install `nvm` and `node` as follows:

* Refer to the [Node Version Manager Documentation]() if this information is out of date
* **Installation** (Choose ONE based on your system OS):
  1. cURL: `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`

  2. Wget: `wget -q0- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash`

  3. The installation will add the following to your `.bashrc` or `.bash_profile` in your `home` directory:

    ```
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion" # This loads nvm bash_completion
    ```

* Run the following command to verify the installation of `nvm`:
  1. run from Terminal: `$ command -v nvm`

  2. Expected Output: `nvm`

* On **macOS**, if you receive and error of `nvm: command not found`, then you need to add the following line to your `.bash_profile` found in your `home` directory as shown below:
  1. `source ~/.bashrc`

* To download, compile, and install a specific version of [Node.js](), then please run the following command to obtain [Node.js v8.10.0]() as needed to be able to work with [AWS Lambda]():
  1. `$ nvm install 8.10.0`

  2. You can list available versions to install using:
    * `$ nvm ls-remote`

  3. The completed output should look like this, showing that you are now ready to start building services in [AWS Lambda]()!

    ![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/NodeInstallComplete4Lambda.png "Complete Node Install with NVM!")

  4. Give yourself a tap on the back. Being able to hit the ground running as a new developer on a new team is a skill many employers would pay a few bucks extra to have more of on the team. Always refer to this page and tell your friends that this is where you can get the *low-down* on how to get it done without having to ask 10 questions on our favorite technology forums out in the ether.

#### Setup Editor and Install Linting

For JavaScript, React.js, and the build process that we are using in [SublimeText3]() we will continue to configure linting, and formatting, while making use of OpenSource libraries and tools to help make this implementation of React.js more efficient. Please take the following steps to complete the installation of `ESLint`:

* **Install ESLint:** Must install **BOTH** Globally & Locally
  1. **Global Install:** `$ npm install -g eslint`

  2. **Local Install:** (Must complete from the `root` of the project directory!!!)
    * `$ npm install --save-dev eslint`

  3. **Local Install of the `babel-eslint` library also:** (Must complete from the `root` of the project directory!!!)
    * `$ npm install --save-dev babel-eslint`

* Verify that you can run `eslint` from within the `local` project directory:
  1. run from Terminal: `$ ./node_modules/.bin/eslint -v`

  2. Expected Output: `v5.15.0 (Or Latest)`

  3. Here is what the output should look like right now:

  ![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/ESLintInstalled.png "Complete ESLint Install!")

From this point forward, you can run: `$ eslint .` and the linter will help you and your development team check syntax, find problems, and enforce code style across your entire organization. In my case, that means just team `Wilson` and I hammering away at the keyboard debating the intricacies of JavaScript Memory Leaks and the best approach to achieve the best string concatenation efficiency. I am sure this is all very relatable. Here is what my code review process looks like when `Wilson` does not use the `eslint` settings I have specifically laid out for you today:

**Wilson: The SCRUM Master**

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/WilsonScrumMaster.png "Wilson: The SCRUM Master")

#### Confirm ESLint Configuration Settings & Attributes

From the project root directory run `$ ls -a`, and confirm that you can see the file called: `~/MyApp/Backend/services/ServerlesStarterService/.eslintrc.js` within the serverless project directory for the service you are implementing. Please look at the structure I have chosen to use as the `$PATH` for this example. Take this as a `hint` for now and we will go over this in detail a bit later. For now, simply open the file from within the `ServerlesStarterService` directory by running `$ subl .eslintrc.js` from your terminal to confirm that the following information is in the file:

```
module.exports = {
  "extends": ["eslint:recommended", "plugin:react/recommended"],
  "parser": "babel-eslint",
  "plugins": ["react"],
  "parserOptions": {
    "ecmaFeatures": {
      "jsx": true
    }
  },
  "env": {
    "node": true
  },
  "rules": {
    "react/jsx-uses-react": 2,
    "react/jsx-uses-vars": 2,
    "react/react-in-jsx-scope": 2,
    "no-alert": 2,
    "no-array-constructor": 2,
    "no-caller": 2,
    "no-catch-shadow": 2,
    "no-labels": 2,
    "no-eval": 2,
    "no-extend-native": 2,
    "no-extra-bind": 2,
    "no-implied-eval": 2,
    "no-iterator": 2,
    "no-label-var": 2,
    "no-labels": 2,
    "no-lone-blocks": 2,
    "no-loop-func": 2,
    "no-multi-spaces": 2,
    "no-multi-str": 2,
    "no-native-reassign": 2,
    "no-new": 2,
    "no-new-func": 2,
    "no-new-object": 2,
    "no-new-wrappers": 2,
    "no-octal-escape": 2,
    "no-process-exit": 2,
    "no-proto": 2,
    "no-return-assign": 2,
    "no-script-url": 2,
    "no-sequences": 2,
    "no-shadow": 2,
    "no-shadow-restricted-names": 2,
    "no-spaced-func": 2,
    "no-trailing-spaces": 2,
    "no-undef-init": 2,
    "no-underscore-dangle": 2,
    "no-unused-expressions": 2,
    "no-use-before-define": 2,
    "no-with": 2,
    "camelcase": 2,
    "comma-spacing": 2,
    "consistent-return": 2,
    "curly": [2, "all"],
    "dot-notation": [2, {
      "allowKeywords": true
    }],
    "eol-last": 2,
    "no-extra-parens": [2, "functions"],
    "eqeqeq": 2,
    "key-spacing": [2, {
      "beforeColon": false,
      "afterColon": true
    }],
    "new-cap": 2,
    "new-parens": 2,
    "quotes": [2, "double"],
    "semi": 2,
    "semi-spacing": [2, {
      "before": false,
      "after": true
    }],
    "space-infix-ops": 2,
    "keyword-spacing": 2,
    "space-unary-ops": [2, {
      "words": true,
      "nonwords": false
    }],
    "strict": [2, "global"],
    "yoda": [2, "never"]
  }
};
```

Please add the `eslintrc.js` file with the information above if you do not have it in your directory as shown above.

Moving forward, we can continue to install the ESLint plugins that we will need to use for our React.js implementations also. In the root of the project directory, run the following two commands to install the React.js plugin for ESLint:

* `$ npm install eslint-plugin-react --save-dev`

* ` $ npm install -g eslint-plugin-react --save-dev` (Install globally also)

Running `$ ./node_modules/.bin/eslint src` (with src being the path to your JavaScript files), will now parse your sources with **Babel** and will provide you with linting feedback to the command line.

We think it's going to be best (and just easiest quite frankly), to just `alias` that last command with something like: `$ npm run lint` as part of your automation approach by adding the following `script` into the `package.json` file that you can find in the root directory of your application:

```
"scripts": {
    "lint": "eslint .",
    ...
  },

  ...
```

* **Run:** `$ npm run lint` to lint your project from the `terminal`.

The linter will now supply feedback on syntax, bugs, and problems, while enforcing code style, all from within the comfort of your `terminal`. Do not fool yourself, this will work in `vim` also! For all those `wq!` fans out there, all hope, is not lost... `#UseTheForce`.

A typical output running ESLint from the `terminal` as instructed would look something like this (depending on your project and the silly errors you make):

![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/npmRunLint.png "$ npm run lint. An example!")


One more thing, from within the project root directory please make sure that you have a file called `.esformatter` in existence. You are going to need that `$ ls -a` command to find it. If it does not exist, go ahead, and create it with a simple `$ touch .esformatter` and `wq!` the following bit of information into the file (if it already exists, just make sure this is in there!):

```
{
  "preset": "default",

  "plugins": [
    "esformatter-quotes",
    "esformatter-semicolons",
    "esformatter-literal-notation",
    "esformatter-parseint",
    "esformatter-spaced-lined-comment",
    "esformatter-var-each",
    "esformatter-collapse-objects",
    "esformatter-remove-trailing-commas",
    "esformatter-quote-props"
  ],

  "quotes": {
    "type": "double"
  },

  "collapseObjects": {
    "ObjectExpression": {
      "maxLineLength": 79,
      "maxKeys": 1
    }
  },

  "indent": {
    "value": "  ",
    "AlignComments": false
  },

  "whiteSpace": {
    "before": {
      "ObjectExpressionClosingBrace": 0,
      "ModuleSpecifierClosingBrace": 0,
      "PropertyName": 1
    },
    "after": {
      "ObjectExpressionOpeningBrace": 0,
      "ModuleSpecifierOpeningBrace": 0
    }
  }
}
```

From here on out every time you save your `JavaScript` files all the formatting completes automatically for you. Sort of, we just must configure all of this into our trusty [SublimeText3]() text editor now!

Before we get into it, yes, you can use `vim`. I promise you, you will find people who will die by `vim` throughout your career. My belief; keep it simple, buy the [SublimeText3]() license and just use that over every other IDE that will bombard your spam folder in your email. [SublimeText3]() provides the simplicity of `vim` without having to memorize the abstract commands like `wq!` that will inevitably leave you with a mess of `*.swp` files, because I guarantee that most of you will never clean them out and it becomes a hassle. Keep it simple, do not over complicate your life in an already all too complicated environment, and get the tool that is really cheap, easy on the eyes, and provides enough of the fancy functionality of a really expensive IDE and the simplicity of `vim` without having to memorize all of the abstract commands: `wq!`

#### SublimeText3 Configuration

To complete the configuration in [SublimeText3]() please install `PackageControl` and the following packages from within [SublimeText3]():

* The easiest way to achieve this is to navigate to the [SublimeText3]() `View` --> `ShowConsole` menu, and proceed to paste the following code provided by [PackageControl](https://packagecontrol.io/installation):

  ```
  # For SublimeText3 ONLY!

  import urllib.request,os,hashlib; 
  h = '6f4c264a24d933ce70df5dedcf1dcaee' + 'ebe013ee18cced0ef93d5f746d80ef60'; 
  pf = 'Package Control.sublime-package'; 
  ipp = sublime.installed_packages_path(); 
  urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); 
  by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); 
  dh = hashlib.sha256(by).hexdigest(); 
  print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) 
  if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
  ```

  The configuration parameters provided above, will generate an `Installed Packages` directory on your `local` machine (if needed). It will download the Package Control.sublime-package over HTTP instead of HTTPS because of known Python standard library constraints, and the file will be validated using SHA-256.

  **WARNING:** Please do not copy or install this code via this tutorial or our website. It will change with every release of [PackageControl](https://packagecontrol.io/installation). Please make sure to view the [Official PackageControl Release Documentation](https://packagecontrol.io/installation) page and installation instructions to get the most recent version of the code shared in this tutorial. You can obtain the most recent information needed directly from: [PackageControl](https://packagecontrol.io/installation).

* Next, please proceed to navigate through to `SublimeText` --> `Preferences` --> `PackageControl` --> `InstallPackages` and install the following tools:

  1. Babel
  2. ESLint
  3. JSFMT
  4. SublimeLinter
  5. SublimeLinter-eslint (Connector)
  6. SublimeLinter-annotations
  7. Oceanic Next Color Scheme
  8. Fix Mac Path (If using MacOS ONLY)

* Once you have completed the above, go ahead and navigate to: `View` --> `Syntax` --> `Open all with current extension as ...` --> `Babel` --> `JavaScript (Babel)` with any `file.js` open to configure the settings for the syntax is `JS` and `JSX`.

* It is helpful to setup a `JSX` formatter for your text editor also. In our case we are using [esformatter-jsx](https://www.npmjs.com/package/esformatter-jsx). You will have to figure out where your `SublimeText3` `Packages` directory is located to complete your `jsfmt` configuration. Run the following commands to complete this step:

  1. `$ cd ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/jsfmt`

  2. `$ npm install jsfmt`
    * Make an attempt to run: `$ npm ls esformatter` before proceeding to step #3

    * If `esformatter` is already installed then skip step #3 and run:
      1. `$ npm install esformatter-jsx`

  3. `$ npm install esformatter esformatter-jsx` (**See notes above before proceeding with this step!!!**)

  4. Test the installation of each package and run: `$ npm ls <package>` (See the expected output below)

    ![alt text](https://github.com/lopezdp/TechnicalArticles/blob/master/img/jsfmt-install.png "$ jsfmt installation complete!")

* From the `jsfmt` package directory (See above if you don't remember! `hint: See Step #1 from above`) run: `$ ls -a` and open a file in `SublimeText3` called: `$ subl jsfmt.sublime-settings` and paste the following configuration settings:




    

















































