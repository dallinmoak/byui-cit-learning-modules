---
title: Organizing - Introduction to Libraries with ES Modules
description: Getting started with using ES modules to create libraries to organize your code and make it more reusable.
date: 2021-10-15

layout: layouts/post.njk
---

## Libraries - sharing your functions with others

A higher order organizational idea in JavaScript is a library. Libraries are a way that you can share your code for other programmers to use in their applications, and you can share your code with them. Libraries are groups of functions that, unlike applications, can not run on their own. Instead, you use what other people have written and compiled as if you wrote it yourself.

In JavaScript, libraries consist of some number of files in which you put your JavaScript. By tradition, the names of your files always ends in '.js'. If I had a JavaScript library called totally_awesome, and in it there was some code that moved stuff around on the screen, I might put that code in a file called 'animations.js'. There would be other files in my library that contained other functions doing other things. Each file would be named after what it does and use the '.js' name ending. For example, fades.js, slideshow.js, etc.

## Purpose

Encapsulation: "The goal of encapsulation is the bundling or co-location of information (data) and behavior (functions) that together serve a common purpose."

The reason developers like working with libraries is that it allows them to group alike program bits together, and selectively limit programmatic access to the parts we consider private details. What's not considered private is then marked as public, accessible to the whole program.

A library should be focused on exposing in a simple way a specific bit of functionality. They should ideally do one thing and do it well.

## ES Modules

Libraries created as described above are simple to make, but do have a few drawbacks. The most important is that everything in them gets added to the global scope with all of the disadvantages that come with that. In the ES6 version of Javascript a new feature was added to help solve this. ES Modules.

Go read this article: [JavaScript Modules: From IIFEs to CommonJS to ES6 Modules](https://ui.dev/javascript-modules-iifes-commonjs-esmodules/). Read down to the section IIFE, if you are interested in some history then read on...if not then skip the next few sections and start again at the ES Modules section. Then come back and finish this article.

First a few important facts about ESModules

- ESModules are based around files...one module per file.
- ESModules are strict by default
- ESModules establish their own private scope.
- Anything that you need access to outside of the module must be **exported**.
- Exports can be **default** (one per module) or **named** (as many as you need)
- You use the `import` command to use a module.
- When you use ESModules you need to let the browser know by adding type="module" to your script tag ie.

  ```javascript
  <script src="main.js" type="module"></script>
  ```

## Example - A module with shared utility functions

If we had a simple module for utility functions it might look like this:

```javascript
// filename: utility.js
// wrapper function for querySelector
export function qs(selector) {
  return document.querySelector(selector);
}

// create an alert at the top of the page for 3 seconds
// requires the message to be displayed and the time in milliseconds.
export function alertMessage(message, duration = 3000) {
  const alert = document.createElement("p");
  alert.innerHTML = message;
  alert.setAttribute(
    "style",
    "background-color:lightpink; border: 1px solid red; position:absolute; top:0; left:0; right:0; padding: 1em;"
  );
  document.body.prepend(alert);
  setTimeout(function () {
    document.body.removeChild(alert);
  }, duration);
}
```

To use this we would import the functions we wanted to use in our main javascript file

```javascript
// main.js...this is the file that you added to the html through a script tag
import { qs, alertMessage } from "./utilities.js";
// now you can use those functions just like if they were declared locally.
alertMessage("I'm from the module!");
```