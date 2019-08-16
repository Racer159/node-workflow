# Node.js Introduction

## So what is this repository?

This repository serves as an introduction to building a basic node application that will be used to create a Discord chatbot. While this should provide a good introduction to node, npm and its various uses, it is strongly recommended to follow up with [W3Schools Online Web Tutorials](https://www.w3schools.com/) which go through many different languages including the use of JavaScript in the browser (something we won't touch on much here). The node reference documentation is also another great place to find tips, tricks, and other guides to getting the most out of node and npm.

## What are JavaScript, Node.js, and NPM?

`JavaScript` (not related to `Java` except by name) was, somewhat famously, created by NetScape's Brendan Eich in 10 days during May of 1995 as something originally conceived to serve as a high-level programming language for use in web browsers (NetScape Navigator only at the time).  Over the decades this language has evolved quite a lot to something that can be used not only in the browser, but also server-side, or even in native applications.  It is even possible to build what are known as polymorphic web applications using JavaScript (which have one codebase sharing its code files across the application's web client, backend server, and native applications).  Because of this transformation, however, JavaScript can sometimes be a mess, with [whydoesitsuck.com](https://whydoesitsuck.com/why-does-javascript-suck/) providing a decent breakdown of some of the core issues.  These issues have led many to create various tools and frameworks to help, which in addition to Node.js and NPM (which we will go over here), I strongly recommend looking into [TypeScript](https://github.com/Microsoft/TypeScript) as well.

`Node.js` is a server-side JavaScript environment that has, for the most part, become the defacto way to run server-side JS.  It can be used to build everything from command-line applications to web servers and tends to excel at networking given its native support for the JavaScript Object Notation (JSON), which is a common web messaging serialization standard.  We will be using it here as the runtime for our chatbot application.

`NPM` stands for Node Package Manager and provides an easy way to install and update dependencies for your node application.  In this way it is similair to other programming language-specific package manager's such as Python's PIP, or .Net's NuGet.

## Getting Started

In order to get started with server-side JavaScript using Node.js and NPM you first need to install Node.js and NPM to your PC, which can be done from here: https://nodejs.org/en/download/.  This tutorial assumes you download the LTS release which at the time of writing was `10.16.3`.  All you need beyond this is a terminal and a text editor, although if you want a more integrated expirience, you can also install [Visual Studio Code]() which is a free Integrated Development Environment (IDE) that is itself written in JavaScript.

Once Node.js, and NPM are installed, you can open a terminal, and create a working directory for this project in your file system using mkdir as below:

```bash
mkdir node-discord-bot
```

You can then `cd` into this directory (or open it in VSCode), and can bootstrap your first Node project by running the command below:

```bash
npm init
```

The `init` command tells NPM that you want to create a new Node module in the current directory, and will ask a series of questions about the project to get you setup.  For now, accepting the defaults will be just fine, and we can go back and edit these later if we need to.

Once this completes, you will see that you have a new file called `package.json`, which is a JSON file that describes your module, its dependencies, and any scripts that you have setup to be ran by NPM (which we will go into more depth on later).

Now we can start the fun part: creating our first javascript application.  In the defaults that were set in the package.json, the main file was called `index.js` so we are going to now go ahead and create that file using the following command:

```bash
touch index.js
```

Now open that file and enter the following to make it output `Hello World!` to the terminal:

```javascript
console.log('Hello World!');
```

And by running the following in the working directory, we can run the JavaScript file:

```
node index.js
```

And that's it, you've now written your first application in JavaScript!  In the next section we will go over installing dependencies and setting up your Discord bot.

## Discord Bot

In order to setup a Discord bot, you will obviously need a Discord account and server.  If you are unfamiliar with Discord, it is a free chat application and server that allows your friends to join a server to chat together.  For our purposes here, it will be used as a playground for our bot.  If you do not want to use Discord, you can create similar bots using other chat services, however we will only touch on Discord here.

To go ahead and create an account, you can do so at the following link:

https://discordapp.com/register


Once this is setup, you will need to create a new bot by opening a new tab and visiting the [Discord Developer Page](https://discordapp.com/developers/applications/) and selecting `New Application`.  From here you can give it a name, and click `Create`, and once this is done you will be brought to a page that shows the information associated with this application including its `Client ID` which we will need to use in a later step.

On this same page, you will also need to setup a bot to live inside of this application which can be done by selecting `Bot` from the left-hand sidebar, then `Add Bot` followed by `Yes do it`.  You will then see a message stating `A wild bot has appeared!` and will be presented with the configuration for your bot, including your `Token` which will be needed within your JavaScript code itself.

Next, you will need to go back to your main Discord tab, and create a new Discord server by selecting the plus button at the bottom of your server list in the left-hand sidebar. From here select `Create a server`, give it a name and region, and click `Create`.

Now you have both a bot and a server, but you haven't joined the two to each other yet.  In order to do this, you will need to create an OAuth URL (a very common authentication mechanism on the web you can learn about [here](https://www.digitalocean.com/community/tutorials/an-introduction-to-oauth-2)) by taking the below URL and replacing the `client_id` with the `Client ID` of your bot from before:

https://discordapp.com/api/oauth2/authorize?scope=bot&client_id=000000000000000000

By visiting this URL in a new tab, you will be brought to a wizard to configure your bot, and from here you can select the server you created earlier, followed by `Authorize`.

## Installing dependencies

To help us talk to our Discord bot from JavaScript, Discord has written a simple node module that we can install into our project and make use of called `discord.js`

This dependency can be installed using the following NPM command:

```
npm install discord.js
```

## Writing the code

Now that we have our project, our Discord bot, and our dependencies set up we can now begin writing the code.

```
const Discord = require('discord.js');
const client = new Discord.Client();
const token = process.env.DISCORD_BOT_TOKEN;

client.on('ready', () => {
  console.log('BOT READY: ' + client.user.username);
});

client.on('message', msg => {
    if (msg.author.id !== client.user.id) {
        msg.channel.send(msg.content.split('').reverse().join(''));
    }
});

client.login(token);
```

## Where to find more information

Thanks to Gareth Dwyer from codementor.io for inspiration for this project: https://www.codementor.io/garethdwyer/building-a-discord-bot-with-node-js-and-repl-it-mm46r1u8y