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

# Structure of the Angular App

* package.json - your project configuration and dependencies

 * Has `ng serve` for starting the app
 
 * Has `ng build` for compiling the apps static assets
 
* angular-cli.json - configurations specific to the Angular CLI

  * Contains ouput directories
  
  * Style sheets
  
  * Script file mappings
  
* node_modules - your modules in the dependencies
  
 * src - HTML files, TypeScript files, Style Sheets
 
  * app subfolder - the application itself
  
    * app.module.ts - where all your components, services and modules are tied together.  Everything needs to be imported to here and then added to the @ngModule directive
    
    * app.component.ts - the main app component, including the AppComponent class
    
    * app.component.html - the main HTML template file
    
 # Components (demonstrative)
 
 * To generate a component in the src/app/components folder (you need to create components if it doesn't exist)
 
 `ng g component components/user`
 
  Generates (the "g" option above) a component named user in src/app/components with its starter TypeScript and HTML files.  It also updates the app.module.ts file adding the new component.
  
  * Your component initialiations should be placed in the ngOnInit() method within the UserComponent class just generated in the user.component.ts file (recommended over the constructor)
  
  * Replace the default HTML in src/app-component.html with `<app-user></app-user>`.  app-user comes from the @Component directive selector: 'app-user' in the app/components/user/user.component.ts file.  Now the browser page shows the default "user works!" text from the user.component.html file. 
  
  * To create a display a property add a name property to the UserComponent class in app/component/user/user.component.ts, ex `name = 'Bill'` and display it through the app/component/user/user.component.html template using double curly brackets, ex `<h1>Hello {{name}}</h1>`
  Note the double curly brackets are referred to as **string interpolation**
  
# Code directives

## ngFor directive

Allows the looping through arrays within the HTML itself

* Example (Assuming the property **hobbies** is defined in the UserComponent class)

```html
<ul>
  <li *ngFor="let hobby of hobbies">{{hobby}}</li>
</ul>
```
This will display a list of hobbies, with one `<li></li>` pair for each hobby
