# Overview

JavaScript notes, particularly as it applies to browsers

# References
* [W3 Schools](https://www.w3schools.com/js/default.asp)
* [ES6 Series](https://www.youtube.com/watch?v=2LeqilIw-28&list=PLillGF-RfqbZ7s3t6ZInY3NjEOOX7hsBv) YouTube series by Traversy Media

# Recent Versions

* ES5/2009 - ECMAScript
* ES6/2015 - ECMAScript.  New features
    * Backward compatible with ES5    
    * **let** and **const** declarations    
    * Classes and inheritance    
    * Template strings    
    * New data structures    
    * Iterators    
    * Promises and Asynchronous data    
    * Arrow functions   

# Functions

Functions in JavaScript in a lot of ways behave like functions in other languages, but they do have some fairly unique characteristics such as function expressions (both named and unnamed), function constructors for creating objects, and self-infoking functions

## Standard functions

```javascript
function sum(x, y) {
  return x + y;
}

let total = sum(200, 550);
```

## Function expressions

```javascript
let func = function (str) {
    console.log('Hello, ' + str);
};

func('world');
```
Note the function variable (func in this case) can also be passed to other functions as parameters.

## Inline function expressions

The inline unnammed function `(item, pos)=>{` is using ES6 arrow function syntax, ES5 function(item, pos) {` syntax is also available

```javascript
// Get rid of duplicate entries in matches array
let uniqueMatches = matches.filter((item, pos)=>{
    return matches.indexOf(item)== pos; 
});
```

## Self-invoking function expressions

The following function will be invoked when the JavaScript file is loaded by the HTML page:

```javascript
(function () {
    console.log('Script loaded');
})();
```
Note the open parenthis at the end is what makes this anonymous function expression self-invoking

## Object methods (using function expressions)

Uses ES6 arrow function syntax here, but the ES5 `fullname: function() {` syntax works as well.

```javascript
// define object literal 
let person = {
  firstName: 'Billy',
  lastName: 'McGilly',
  fullName: () => {
      return this.firstName + ' ' + this.lastName;
  }

// call the object literal's method fullName()
console.log('fullName: ' + person.fullName());
```
Note that the same principle and basic technique applies to other object types, not just object literals

## Function Constructors

You can create objects using what is referred to as function constructors

```javascript
function person(first, last) {
    this.firstName = first;
    this.lastName = last;
    this.fullName = () => {
        return this.firstName + ' ' + this.lastName;
    };
}

let person1 = new person('John', 'Doe');
let person2 = new person('Sally', 'Rally');

console.log(person1.fullName());
console.log(person1.fullName());
```

# Tips and Tricks

## Stopping a form from triggering a submit action

When a form is submitted it it reloads the entire page, which is often not desired, particularly when calling scripts that only update a portion of the page (violates the AJAX intent for example), or you don't want your initial on load code to be re-executed.

* Simple solution (return false to onSubmit)

```html
<form class="dialog" onsubmit="return false">

  ...
  <input id="submit" type="submit" onclick="doSomething()" value="Submit">
</form>
```

* Have your code decide whether to submit or not (true = yes submit, false means don't)

```html
 <form class="dialog" onsubmit="return doSomething()">

    ...
    <input id="submit" type="submit" value="Submit">
 </form>
```

* Have your code cancel the submit event

```javascript
let form = document.getElementById("FormID");

 form.addEventListener("submit", (e) => {
      if ("Your Desired Conditions.") {
          e.preventDefault();
      }
 });
```

* Canceling the submit event with JQuery

```javascript
$('#formId').submit(function (evt) {
    evt.preventDefault();
    window.history.back();
});
```

# Regular Expressions

## RegExp

RegExp is a regular expression object with methods and properties to detail with regular expressions

### Creating a RegExp object

A regular expression can be assigned directly to a variable, with that variable becoming of type RegExp
```javascript
let regEx = /exp/g
```

It can also be created with **new** using the RegExp constructor.  The second parameter is optional and provides flags ("g" = global, "m" = multiline, "i" = ignore case)
```javascript
let regEx = new RegExp(/exp/, 'gm');
```
This method is useful when you want to combine multiple components (strings and other regular expressions).  For example,

```javascript
let wBound = /\b/;
let regEx = new RegExp(wBound.source + '^Test(ing|er|ed)$' + wBound.source, 'gm');
```
Using a string literal above but more typical a string variabe, possibly from a web form.  Note the use of the **.source** property.  Without this it would not work correctly because the concatentated expression would double up the **/** delimiters.

### Partial list of the methods

* **RegExp.exec(string)** - invoke to return a match within the string parameter based on the regexp regular expression.  It returns an array containing the results, or null if nothing found.  Element zero of the returned result is the matched text itself, while 1 thru n is the captured substrings if the regEx search includes groups.  The array also contains the "index" for the beginning location of where the match was foun.  If the global flag was set it will also iclude a .lastIndex property value where the next invokation of exec() will start when running it in a loop.

  Example loop with exec() - You would use this if your expression includes a global (multi match) flag
  
  ```javascript
  while ( (match = regex.exec(targetText)) !== null) {
    // match[0] contains the match itself
    // here storing a list of the matches
    matches.push(match[0]); 

    ...

    // if there are any capture groups in the expression this will display each one
    for (let i = 1; i < match.length; i++) {
        if (match[i] !== undefined & match[i] !== '') {
            output += `<li>element ${i}: ${match[i]}</li>`;                       
        }  
    }
    output += '</ul>';

    //console.log(match);
    if (matchCount++ > matchLimit) {
        break;
    }
  } 
  ```
  
* **RegExp.source** - contains the text version of the regular expression without the **/** delimiters and flags.  Useful when concatenating multiple component pieces of the expression.
  
* **RegExp.lastIndex** - when searching for multipe potential matches (with the "g" global flag) this will indicate where the next iteration of **RegExp.exec()** should start (in effect the end of the prior match + 1)

## Converting text from the DOM into a RegExp object

```javascript
let targetText = document.getElementById('data').value;
let regex = new RegExp(document.getElementById('regex').value, 'gm');
```

# Chrome Tools and JavaScript Examples

Note: most of the notes in this section are from the [LearnWebCode](https://www.youtube.com/watch?v=zPHerhks2Vg&t=302s) YouTube video.

The **Chrome Developer** Tools (right-click the page then select Inspect)is useful for running JavaScript interactively with the session.

* On the console enter these as an examples (note the ending semi-colon not required):

   ```
   window
   ```
   Displays the Window object with a navigatable tree of its subcomponents.

   ```
   document
   ```
   Displays the document object with a navigatable tree of its subcomponents.

   ```
   document.title
   ```
   Displays the document title.  You can also set the title here in the console, e.g. `document.title = "Test"`

   ```
   document.getElementById("filename").value;
   ```
   Assuming you have an element with an id of "filename" it displays this elements **value attribute**, useful for example with text input elements.

   ```
   document.getElementById("output").innerHTML = "This is a test";
   ```
   Assuming you have an element with an id of "output" it sets this elements innerHTML, useful for many elements.

* Console output from JavaScript files

   You can write to the Chrome console from any JavaScript (whether separate file or in the HTML) with `console.log("message");`

# More Examples (using script files instead of console)

* To get elements by TagName ("p", "ul", "li", etc) within a parent element (ex: the \<ul\> parent of the\<li\>) selected by class

   ```
   var listItems = document.getElementById("theUlTagId").getElementsByTagName("li");
   for (i = 0; i < 4; i++) {
       listItems[i].style.color = "red";
   }
   ```
   This will assign an array of all the \<li\> elements, which can then be accessed individually by index, e.g. `listItems[0]`
