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

```
mkdir node-discord-bot
```

You can then `cd` into this directory (or open it in VSCode), and can bootstrap your first Node project by using the command below:

```
npm init
```

Running this command tells NPM that you want to create a new Node module in the current directory, and will ask a series of questions about the project to get you setup.  For now, accepting the defaults will be just fine.

Once this completes, you will see that you have a new file called `package.json`, which is a JSON file that describes you module, its dependencies, and any scripts that you have setup to be ran by NPM (more on this later).


