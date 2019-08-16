# Node.js Introduction

## So what is this repository?

This repository serves as an introduction to building a basic node application that will be used to create a Discord chatbot. While this should provide a good introduction to node, npm and its various uses, it is strongly recommended to follow up with [W3Schools Online Web Tutorials](https://www.w3schools.com/) which go through many different languages including the use of JavaScript in the browser (something we won't touch on much here). The [Node.js reference documentation](https://nodejs.dev/) is also another great place to find tips, tricks, and other guides to getting the most out of Node.js and NPM.

## What are JavaScript, Node.js, and NPM?

`JavaScript` (not related to `Java` except by name) was, somewhat famously, created by NetScape's Brendan Eich in 10 days during May of 1995 as something originally conceived to serve as a high-level programming language for use in web browsers (NetScape Navigator only at the time).  Over the decades this language has evolved quite a lot into something that can be used not only in the browser, but also server-side, or even in native applications.  It is even possible to build what are known as polymorphic web applications using JavaScript, which have one codebase sharing its code files across the application's web client, backend server, and native applications.  Because of this transformation, however, JavaScript can sometimes be a mess, with [whydoesitsuck.com](https://whydoesitsuck.com/why-does-javascript-suck/) providing a decent breakdown of some of the core issues.  These issues have led many to create various tools and frameworks to help, which in addition to Node.js and NPM (which we will go over here), I strongly recommend looking into [TypeScript](https://github.com/Microsoft/TypeScript) as well.

`Node.js` is a server-side JavaScript environment that has, for the most part, become the defacto way to run server-side JS.  It can be used to build everything from command-line applications to web servers and tends to excel at networking given its native support for the JavaScript Object Notation (JSON), which is a common web messaging serialization standard.  We will be using it here as the runtime for our chatbot application.

`NPM` stands for Node Package Manager and provides an easy way to install and update dependencies for your node application.  In this way it is similair to other programming language-specific package manager's such as Python's PIP, or .Net's NuGet.

## Getting Started

In order to get started with server-side JavaScript using Node.js and NPM you first need to install Node.js and NPM to your PC, which can be done here: https://nodejs.org/en/download/.  This tutorial assumes you download the LTS release which at the time of writing was `10.16.3`.  All you need beyond this is a terminal and a text editor, although if you want a more integrated expirience, you can also install [Visual Studio Code](https://code.visualstudio.com/) which is a free Integrated Development Environment (IDE) that is itself written in JavaScript.

Once Node.js, and NPM are installed, you can open a terminal, and create a working directory for this project on your file system using mkdir as below:

```bash
mkdir node-discord-bot
```

You can then `cd` into this directory (or open it in VSCode), and can bootstrap your first Node project by running the following:

```bash
npm init
```

The `init` command tells NPM that you want to create a new Node module in the current directory, and will ask a series of questions about the project to get you setup.  For now, accepting the defaults will be just fine, and we can go back and edit these later if we need to.

Once this completes, you will see that you have a new file called `package.json`, which is a JSON file that describes your module, its dependencies, and any scripts that you have setup to be ran by NPM.

Next we can start the fun part: creating our first javascript application.  In the defaults that were set in the package.json, the main file was called `index.js` so we are going to now go ahead and create that file using the following command:

```bash
touch index.js
```

Now open that file and enter the following to make it output `Hello World!` to the terminal when it is ran:

```javascript
console.log('Hello World!');
```

And by running the following in the working directory, we can run the JavaScript file to see its output:

```
node index.js
```

And that's it, you've now written your first application in JavaScript!  In the next section we will go over setting up your Discord bot.

## Discord Bot

In order to setup a Discord bot, you will obviously need a Discord account and server.  If you are unfamiliar with Discord, it is a free chat application and server that allows your friends to talk and chat together.  For our purposes here, it will be used as a playground for our chatbot so that we can send messages for it to respond to.  If you do not want to use Discord, you can create similar bots using other chat services, however we will only touch on Discord in this tutorial.

To go ahead and create an account, you can do so at the following link:

https://discordapp.com/register


Once you have registered, you will need to create a new Discord deverloper application by opening a new tab and visiting the [Discord Developer Page](https://discordapp.com/developers/applications/) and selecting `New Application`.  From here you can give it a name, and click `Create`, and once this is done you will be brought to a page that shows the information associated with this application including its `Client ID` which we will need to use here in a later step.

On this same page, you will also need to setup a bot to be used with this application which can be done by selecting `Bot` from the left-hand sidebar, then `Add Bot` followed by `Yes do it`.  You will then see a message stating `A wild bot has appeared!` and will be presented with the configuration for your bot, including your `Token` which will be pulled into your JavaScript code through a local environment variable later on.

Next, you will need to go back to your main Discord tab, and create a new Discord server by selecting the plus button at the bottom of your server list in the left-hand sidebar, and from here select `Create a server`, give it a name, a region, and click `Create`.

Now you have both a bot and a server, but you haven't joined the two together yet.  In order to do this, you will need to create an OAuth URL (a very common authentication mechanism on the web you can learn about [here](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)) by taking the below URL and replacing the `client_id` with the `Client ID` of your bot from before:

https://discordapp.com/api/oauth2/authorize?scope=bot&client_id=000000000000000000

By visiting this URL in a new tab, you will be brought to a wizard to configure your bot, and from here you can select the server you created earlier, followed by `Authorize`.

Once this is complete all that is left to do is to add the Bot's Token to your local environment by either running the following command in the terminal, or adding it to your `~/.bashrc` (Linux) or `~/.bash_profile` (macOS).

```bash
export DISCORD_BOT_TOKEN="Kyuufsf9898.382dsfSAFew.87adsfasjdbfhkewry3289aisdfasdflw.sadfw"
```

## Installing dependencies

Now its time to setup our Node app's dependencies.  To help us talk to our Discord bot from JavaScript, Discord has written a simple node module that we can install into our project called `discord.js`.  This will allow us to create a client and send and receive messages, and more information about it can be found [here](https://discord.js.org/#/).

This dependency can be installed using the following NPM command:

```
npm install --save discord.js
```

This will both install the `discord.js` dependency to our local machine in the `./node_modules` folder, but the `--save` option will also add this dependency to our local `package.json` file so that if we pull our application onto another machine, all we need to do is run `npm install` to install all of its related dependencies.

## Writing the code

Now that we have our project, our Discord bot, and our dependencies set up we can now begin writing the code.

Out first step is to delete our `Hello World!` console.log and write the following to import our `discord.js` dependency using the Node.js [require](https://www.freecodecamp.org/news/requiring-modules-in-node-js-everything-you-need-to-know-e7fbd119be8/) syntax.

```javascript
const Discord = require('discord.js');
```

This will pull in the `discord.js` dependency and assign it to a constant so that we can make use of it within our bot.

Next we create another constant that will act as the Discord Client for our bot by instantiating a new instance of the Discord Client from the `discord.js` dependency:

```javascript
const client = new Discord.Client();
```

This will allow us to setup our our bots functionality, and to interact with the Discord API.

Now we can create a third constant that will pull the `DISCORD_BOT_TOKEN` that we put into our local environment earlier into our bot.  This is done using the built in Node.js `process` command that allows you to access various aspects of your local environment (more about it can be found [here](https://nodejs.org/api/process.html));

```javascript
const token = process.env.DISCORD_BOT_TOKEN;
```

Now as an aside, as you can see from the above lines, JavaScript does not make use of types (as you might see in C or Java), and instead variables are declared either by using `const` or `let` in newer apps for constants and normal variables respectively or by the older `var` syntax in older apps.  This lack of type safety requires JavaScript to compensate by making use of some extremely aggressive typecasting (the results of which can be seen in the example below).

```javascript
const numberTwo = 2;
const stringTwo = '2';
const arrayTwo = [2, 2];

const sum = numberTwo + stringTwo + arrayTwo;

console.log(sum); // 222,2
```

This is one of many quirks mentioned above that ecan make JavaScript tricky to work with, and are the reason things like TypeScript exist.

Moving back to our `index.js` file, we now need to add our first callback function so that the application can notify us when the client is ready.  Callbacks in JavaScript are functions that you pass into other functions to be called when something happens.  They are very often found in asynchronous tasks such as this where a client needs to notify when it is ready after logging in.  More about callbacks in JavaScript can be found [here](https://codeburst.io/javascript-what-the-heck-is-a-callback-aba4da2deced), and it is important to note that the below is only one way to deal with asynchronous code in JavaScript.  While we won't get into it here for time's sake, know that there also exist [Promises](https://codeburst.io/javascript-promises-explained-with-simple-real-life-analogies-dd6908092138) which allow you to avoid some of the pitfalls of callbacks (such as [callback hell](http://callbackhell.com/)), and can support newer syntax methodologies such as [async/await](https://javascript.info/async-await).

```javascript
client.on('ready', () => {
  console.log('BOT IS READY: ' + client.user.name);
});
```

Running the code at this point won't do anything because the callback function we created `() => { ... }` won't be called until the client actually logs in.  In order to get this to happen, we need to add the following line to our file:

```javascript
client.login(token);
```

This will login to Discord using the `DISCORD_BOT_TOKEN` environment variable and if it is successful will fire the `ready` event that will cause our callback to run.  Running the code at this point should yield the following:

```
BOT IS READY: <bot-name>
```

We've got a bot!  Now lets make it do something.  To accomplish this, we need to add another callback to our file for the `message` event.  This function accepts a message object and inside we will use an `if` statement to check that the message isn't coming from us (otherwise it would be an infinite loop) before sending a new message to that same channel that is the reverse of the text that was initially sent.

```javascript
client.on('message', (msg) => {
    if (msg.author.id !== client.user.id) {
        msg.channel.send(msg.content.split('').reverse().join(''));
    }
});
```

The last interesting thing to note here is the equality check within the `if` statement having a second equals sign in the not-equals operator.  This again goes back to the agressive typecasting of JavaScript and provides a way for us to check both type and equality.  This can be seen in the example below:

```javascript
console.log(100 == '100');    // true
console.log(100 === '100');   // false
console.log('100' === '100'); // true
```

In the end, all of this comes together to create a short file that looks like the following:

```javascript
const Discord = require('discord.js');

const client = new Discord.Client();
const token = process.env.DISCORD_BOT_TOKEN;

client.on('ready', () => {
  console.log('BOT IS READY: ' + client.user.name);
});

client.on('message', (msg) => {
    if (msg.author.id !== client.user.id) {
        msg.channel.send(msg.content.split('').reverse().join(''));
    }
});

client.login(token);

```

And that's it!  You can now start your bot, and see it respond to everything you say with reversed text!

## Where to go from here

From here you can continue to play with your Node.js Discord Bot, add queries for it to respond to, or even try to call out to APIs using the Node.js [http](https://nodejs.org/api/http.html) library. A good resource for a list of free APIs is available at the following URL: https://apilist.fun/

Also, thanks to Gareth Dwyer from codementor.io for inspiration for this project: https://www.codementor.io/garethdwyer/building-a-discord-bot-with-node-js-and-repl-it-mm46r1u8y