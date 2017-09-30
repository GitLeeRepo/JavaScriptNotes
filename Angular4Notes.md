# Overview

Notes on the Angular 4 JavaScript framework

# References

* [Angular 4 in 60 Minutes](https://www.youtube.com/watch?v=KhzGSHNhnbI) YouTube video by Traversy Media.  Many of the notes here are from following along with this video.

# What is Angular

* Front-end/Client-side JavaScript framework

* Created and maintained by Google

* Part of the MEAN Stack (MongoDB, ExpressJS, Angular, Node.js)

# What Angular is NOT

* Not a server-side platform

* Not a JavaScript libarary (jQuery, React, etc)

* Not a design pattern like MVC

* Not a platform or language (.NET, Java)

# Why use Angular over plain JavaScript?

* Rapid Development & Code Generation with the Angular CLI

* Code Organization & Productivity (encapsolated components)

* Dynamic Content - use code directly in HTML using directives

# Core features and common terms

* Components

* Services

* Routing

* Data Binding

* Templating

* HTTP Module

* Observables

* Directives

* Types

* Events

# TypeScript

Angular uses TypeScript rather than JavaScript itself

* A superset of JavaScript

* Optional Static types

* Class based / Object Oriented

# Components

 Components are sections of the user interface and are the building blocks of an Angular App
 
 * An Angular application is a tree of **components**
 
 * **Decorators** mark HTML classes as Angular components

# Installation

* Node.js must be installed first in order to use the NPM package manager.  Refer to [NodeJsNotes](https://github.com/GitLeeRepo/NodejsNotes/blob/master/NodejNotes.md#overview) for info on this.

* Run npm to install Angular globally

`npm install -g @angular/cli`

* Create the initial application specific framework

 * Create and switch to the project folder
 
 * To initialize an app called a4app
 
 `ng new a4app`

* Change to the generated app folder (a4app in this case)

* Run ng serve to start the development server on port 4200 by default

`ng serve`

* Load the intial app in the browsers at `localhost:4200` to verify installation


