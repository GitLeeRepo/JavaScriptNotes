# Overview

Notes on the Angular 4 JavaScript framework

Note: The actual code written while creating these notes is in the [Angular4Demo01](https://github.com/GitLeeRepo/Angular4Demo01) repository

# References

* [Angular 4 in 60 Minutes](https://www.youtube.com/watch?v=KhzGSHNhnbI) YouTube video by Traversy Media.  Many of the notes here are from following along with this video.

## My Other Notes

* [JavaScriptNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/JavaScriptNotes.md#overview)
* [RestApiNotes](https://github.com/GitLeeRepo/RestApiNotes/blob/master/RestApiNotes.md#overview)

# What is Angular

* Front-end/Client-side JavaScript framework
* Created and maintained by Google
* Part of the MEAN Stack (MongoDB, ExpressJS, Angular, Node.js)

# What Angular is NOT

* Not a server-side platform
* Not a JavaScript library (jQuery, React, etc)
* Not a design pattern like MVC
* Not a platform or language (.NET, Java)

# Why use Angular over plain JavaScript?

* Rapid Development & Code Generation with the Angular CLI
* Code Organization & Productivity (encapsulated components)
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

  ```
  npm install -g @angular/cli
  ```

* Create the initial application specific framework
* Create and switch to the project folder 
* To initialize an app called a4app
 
  ```
  ng new a4app
  ```

* Change to the generated app folder (a4app in this case)
* Run ng serve to start the development server on port 4200 by default

  ```
  ng serve
  ```

* Load the initial app in the browsers at `localhost:4200` to verify installation

# Structure of the Angular App

* package.json - your project configuration and dependencies
 * Has `ng serve` for starting the app 
 * Has `ng build` for compiling the apps static assets 
* angular-cli.json - configurations specific to the Angular CLI
  * Contains output directories  
  * Style sheets  
  * Script file mappings  
* node_modules - your modules in the dependencies  
 * src - HTML files, TypeScript files, Style Sheets 
  * app subfolder - the application itself  
    * app.module.ts - where all your components, services and modules are tied together.  Everything needs to be imported to here and then added to the @ngModule directive    
    * app.component.ts - the main app component, including the AppComponent class    
    * app.component.html - the main HTML template file
    
 # Components (demonstrative)
 
 * To generate a component in the src/app/components folder (you need to create the components folder if it doesn't exist)
 
   ```
   ng g component components/user
   ```
 
  Generates (the "g" option above) a component named user in src/app/components with its starter TypeScript and HTML files.  It also updates the app.module.ts file adding the new component.  
* Your component initialization should be placed in the ngOnInit() method within the UserComponent class just generated in the user.component.ts file (recommended over the constructor)  
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

  To include an index

  ```html
  <ul>
    <li *ngFor="let hobby of hobbies; let i = index">{{i + 1: }} {{hobby}}</li>
  </ul>
  ```
  This will prefix each hobby with a number (the index + 1), so starting at 1

# Events

## Click event

* In the user.component.html

  ```html
  <button (click)="onClick()">Click here</button>
  ```

* In the user.component.ts

  ```typescript
  export class UserComponent implements OnInit {

    ...

    onClick(){
      console.log('Clicked');
    }
  }
  ```

## Form Submit event

* In the user.component.html

  ```html
  <form (submit)="addHobby(hobby.value)">
    <div>
      <label for="hobby">Hobbie: </label>
      <input type="text" #hobby>
    </div>
  </form>
  ```
 Note the `#hobby` tag on the input ISS used in the event signature `addHobby(hobby.value)`

* In the user.component.ts

  ```typescript
  export class UserComponent implements OnInit {

    ...

    addHobby(hobby){
      this.hobbies.push(hobby);
      return false; // prevent the new item from disappearing due to a refresh to the orig
    }
  }
  ```

## Processing a delete through a click event

* In the user.component.html

  ```html
    <li *ngFor="let hobby of hobbies">{{hobby}} <button (click)="deleteHobby(hobby)">x</button></li>
  ```
  Added the `<button></button>` with the click event to the existing `<li></li>`

* In the user.component.ts

  ```typescript
  export class UserComponent implements OnInit {

    ...

    deleteHobby(hobby){
      for (let i = 0; i < this.hobbies.length; i++){
        if (this.hobbies[i] == hobby) {
          // remove from array
          this.hobbies.splice(i, 1);
        }
      }
    }
  }
  ```

# Two way data binding

Binds data in the HTML template to the component, with changes being reflected in both directions

* Need to use ngmodel which requires the forms module to be imported to **app.module.ts**

  ```typescript
  import { FormsModule } from '@angular/forms'

  ...

  @NgModule({
    declarations: [
      AppComponent,
      UserComponent
    ],
    imports: [
      BrowserModule,
      FormsModule
    ],
    providers: [],
    bootstrap: [AppComponent]
  })
  ```
  Note the FormsModule must be both imported and placed in the **imports:** section of the **@NgModule** directive.

* Within user.component.html add the two way binding notation

  ```html
  <form>
    <div>
      <label for="name">Name: </label>
      <input type="text" [(ngModel)]="name" name="name">
    </div>
    ...
    <div>
      <label for="city">City: </label>
      <input type="text" [(ngModel)]="address.city" name="city">
    </div>
    ...
  </form>
  ```
  Now whenever the name on the form is changed the component property "name" will also be updated and displayed wherever it is used.  Note this is dynamic as you type each letter, it does not require a form submit.  Note the `[(ngModel)]="name"` syntax for establishing the two way binding.  Also note the name attribute is also set

  Note that because "city" is part of the address object it must be fully qualified as "address.city" in the Angular two way bind (`[(ngModel)]`), but not in the HTML name attribute

# Services

* Description from [Angular Docs](https://docs.angularjs.org/guide/services)

  AngularJS services are substitutable objects that are wired together using dependency injection (DI). You can use services to organize and share code across your app.

  AngularJS services are:

    * Lazily instantiated – AngularJS only instantiates a service when an application component depends on it.
    * Singletons – Each component dependent on a service gets a reference to the single instance generated by the service factory.


## Built in Services

Angular has about 30 built in services, a few examples are:

* $http

  Importing to app.module.ts and adding to **imports:** section of the @NgModule directive

  ```typescript
  import { HttpModule } from '@angular/http';

  @NgModule({
    declarations: [
      AppComponent,
      UserComponent
    ],
    imports: [
      BrowserModule,
      FormsModule,
      HttpModule
    ],
    providers: [DataService],
    bootstrap: [AppComponent]
  })
  ```

* $location

  Location service. No example at this time

## Creating your own service

* To generate a service in the src/app/services folder (you need to create the services folder if it doesn't exist)
 
  `ng g service services/data`

   Generates (the "g" option above) a component named user in src/app/components with its starter TypeScript and HTML files.  

   Unlike components it does not update the app.module.ts file, it must be added manual.

* Adding the service to app.module.ts
  
  ```typescript
  import { DataService } from './services/data.service';

  @NgModule({
    declarations: [
      AppComponent,
      UserComponent
    ],
    imports: [
      BrowserModule,
      FormsModule
    ],
    providers: [DataService],
    bootstrap: [AppComponent]
  })
  ```
  Note the DataService must be both imported and added to the **providers:** section of of the @NgModule directive.

* Add the service to the **app/components/user/user.component.ts file**

  ```typescript
  import { DataService } from '../../services/data.service';
  ...
  export class UserComponent implements OnInit {
    ...
    constructor(private dataservice:DataService) { 

    }
  ```
  Note the DataService is both imported and included as a parameter to the constructor for the UserComponent class

* Now adding the following in the **DataService class** in **app/services/data/data.service.ts** should output to the browser console if the prior steps were followed

  ```typescript
  import { Injectable } from '@angular/core';
  import { Http } from '@angular/http';
  import 'rxjs/add/operator/map';

  @Injectable()
  export class DataService {

    constructor() { 
      console.log("Data Service connected");
    }

    getPosts() {
      return this.http.get('https://jsonplaceholder.typicode.com/posts').map(res=>res.json());
    }
  }
  ```
  Note this example uses a custom getPosts() method to retrieve JSON data from a RESTful API.  Here it uses the .map() method from the `import 'rxjs/add/operator/map'` to handle the JSON data.  It also uses the Http modules which is one of the built in services to make the AJAX call (GET in this case).

# Router

Use the **router** to use different URLs for different components.

## Create Routes to components

* Create a 2nd component to use as an example

  ```
  ng g component components/about
  ```

 * Add Router/Routes to **app.module**

   ```typescript
   import { RouterModule, Routes} from '@angular/router'

   const appRoutes:Routes = [
     {path:'', component:UserComponent},
     {path:'about', component:AboutComponent}
   ]

   @NgModule({
     declarations: [
       AppComponent,
       UserComponent,
       AboutComponent
     ],
     imports: [
       BrowserModule,
       FormsModule,
       HttpModule,
       RouterModule.forRoot(appRoutes)
     ],
     providers: [DataService],
     bootstrap: [AppComponent]
   })
   ```
   Note the creation of the appRoutes constant which is used in the **imports:** section with the RouterModule, i.e. `RouterModule.forRoot(appRoutes)`

* Add some about HTML content to **app/components/about/about.component.html**
* Replace the `<app-user></app-user>` text with `<router-outlet></router-outlet>` in **app.module.html**
* For the localhost:4200 you still see the UserComponent content, but if you select localhost:4200/about you see the AboutComponent content.
* Adding routerLinks to the two components in **app.component.html**

  ```html
  <ul>
    <li><a routerLink="/">Home</a></li>
    <li><a routerLink="about">About</a></li>
  </ul>
  <router-outlet></router-outlet>
  ```
