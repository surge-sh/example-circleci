# CircleCI example [![Circle CI](https://circleci.com/gh/surge-sh/example-circleci.svg?style=svg)](https://circleci.com/gh/surge-sh/example-circleci)

An example using [CircleCI](https://circleci.com) for continuous deployment to [Surge.sh](https://surge.sh).

## Getting started

Continuous Deployment services like [CircleCI](https://circleci.com) make it possible to run publish your project on Surge each time you push to a GitHub repository.

This guide will walk you through:

1. Getting your Surge token, so CircleCI can login to Surge on your behalf
2. Adding Surge as a `devDependency`, so CircleCI can install Surge
3. Setting up your project on CircleCI, so you can publish each time you push to GitHub

First, you’ll need your token from the Surge CLI. This secret key lets services like CircleCI login and publish projects on your behalf. Get your Surge token by running the following command in your terminal:

```
surge token
```

You’ll be asked to login again, and afterwards your token will be displayed like this:

```
token: a142e09a6b13a21be512b141241c7123
```

![Getting your token from the Surge CLI.](http://localhost:5001/images/help/integrating-with-circleci.gif)

### Adding Surge as a `devDependency` to a `package.json` file

CircleCI’s machines won’t have Surge installed by default, so you also need to save Surge as a development dependency in your project. This lets CircleCI know it needs to install Surge to publish your project.

You can do this by creating a `package.json` file if you don’t have one already. Run the following command in your terminal to be walked through making this file (you can hit enter to accept the defaults):

```sh
npm init
```

You will end up with a file that looks [something like this one](package.json).

Next, run this command to save Surge as a `devDependency`, so CircleCI will install it:

```sh
npm install --save-dev surge
```

#### Double-check your tests

If you needed to add a new `package.json` file, you’ll want to make one small change. It’s possible your initial build will fail if you don’t have any tests, or if you have the default test command in your `package.json`.

You can add tests or just clear this out of your `package.json` file entirely, changing:

```sh
"scripts": {
  "test": "echo \"Error: no test specified.\" && exit 1"
}
```

…into:

```sh
"scripts": {
  "test": "echo \"Error: no test specified.\""
}
```

Commit this change, and push it to your repo. Now, even if you don’t have tests, CircleCI will be able to move onto the deployment command.

### Add your project’s repository to CircleCI

Now you can login and setup a new project on CircleCI. Choose the GitHub organisation your project is in (_surge-sh_ in this example) and then build your project’s GitHub repository:

![Add the GitHub repository your project is stored in. This example is using the surge-sh/example-circleci repo.](http://localhost:5001/images/help/integrating-with-circleci-2.png)

### Add Environment Variables

Choose _Environment Variables_ from your project settings, and you’ll be able to secretly add your email address and token so CircleCI can login to Surge for you:

Create one environment variable called:

```
SURGE_LOGIN
```

…and set it to the email address you use with Surge.

![Adding SURGE_TOKEN` as an environment variable.](http://localhost:5001/images/help/integrating-with-circleci-3.png)

Next, add another environment variable called:

```
SURGE_TOKEN
```

…and set it to your Surge token.

![Adding SURGE_TOKEN` as an environment variable.](http://localhost:5001/images/help/integrating-with-circleci-4.png)

## Run Surge on CircleCI

Now you’re ready to run your deployment step with `surge` on CircleCI.


***

Now, when you push your project to GitHub again, this command will be run and your project will get published automatically.

## License

[The MIT License (MIT)](LICENSE.md)

Copyright © 2015 [Chloi Inc.](http://chloi.io)
