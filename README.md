# Intro to Node

## Introduction
The following is based on an in-person event, but has also been written in such a way that anyone could pick it up and code along! In this short lesson, we'll be build a simple API based on the "official" (unofficial) Star Wars API called [SWAPI](https://swapi.co/)! In the past we built a front-end application that uses this API and you can find that lesson [here](https://github.com/projectshft/swapi).

## Prerequisites
We're going to assume that you're a bit familiar JavaScript and how the internet works. If not, you may be a little lost, but we challenge you to give it a shot either way. At the very least, this code-along should give you an idea of things to learn next!

## Setup
For simplicity sake, we're going to be using [repl.it](repl.it). Navigate to [this link](https://repl.it/@AaronHayslip/Star-Wars-API) to get started. The first thing you'll want to do is click "fork" at the top, middle of the page:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-3.50.29-PM.png)

This will allow you to have your own copy of our project. Okay, before we move on, we have a ton to talk about.

## What is Node and Why is it Useful?
Wikipedia says, "Node.js is an open-source, cross-platform JavaScript run-time environment that executes JavaScript code outside of a browser."

What does that mean?

JavaScript is almost always thought of as being run in the browser, but with Node, we can execute JavaScript outside of the browser. Why is this awesome? Well, it allows us to run Node in new environments to do awesome things like, create web servers.

And what exactly does that mean?

With Node, we don't have to learn Java, Ruby, Python, etc to write code for the "back end" - we can use JavaScript to do that too, just like we do with the front-end! We're not only _able_ to use JavaScript on the back-end with Node, but thanks to Node, writing JavaScript on the back-end is super fast and performant. Node enables JavaScript to be a first-class server-side langauge.

## Running JavaScript
Like we said, the usual place to run JavaScript is in the browser. Assuming you have Google Chrome installed, open in it up and navigate to `view` --> `Developer` --> `JavaScript Console`. It will open a window that looks something like this:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-7.54.08-PM.png)

And now we can write JavaScript!

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.01.15-PM.png)

But this isn't Node. Inside the Chrome browser, there's a JavaScript enginge called the [V8 JavaScript Engine](https://v8.dev/). But, thanks to Node, you can now get this engine locally on your machine by downloading node.

## Downloading Node
For the sake of this lesson, we're going to be using repl.it, but in case you were wondering about how to up and running with Node, it's pretty simple. Just download it from [nodejs.org](https://nodejs.org/en/), install it and open your command-line, then type in `node`, like this:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.05.28-PM.png)

Now, just like with the Chrome Developer Console, we can type in JavaScript and have it executed right from our machine:

![img](https://www.projectshift.io/wp-content/uploads/2018/11/Screen-Shot-2018-11-27-at-8.06.43-PM.png)

But let's get on with building out our API.

## The Star Wars API
