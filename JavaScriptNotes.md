# Overview

JavaScript notes, particularly as it applies to browsers

# References

* [W3 Schools](https://www.w3schools.com/js/default.asp)
* [ES6 Series](https://www.youtube.com/watch?v=2LeqilIw-28&list=PLillGF-RfqbZ7s3t6ZInY3NjEOOX7hsBv) YouTube series by Traversy Media

## My Other Notes

* [AjaxNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/AjaxNotes.md#overview)
* [Angular4Notes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/Angular4Notes.md#overview)
* [JsonNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/JsonNotes.md#overview)
* [ESLintNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/ESLintNotes.md#overview)
* [NodejNotes](https://github.com/GitLeeRepo/NodejsNotes/blob/master/NodejNotes.md#overview)
* [PHPNotes](https://github.com/GitLeeRepo/PHPNotes/blob/master/PHPNotes.md#overview)
* [PythonNotes](https://github.com/GitLeeRepo/PythonNotes/blob/master/PythonNotes.md#overview)
* [WordPressNotes](https://github.com/GitLeeRepo/WordPressNotes/blob/master/WordPressNotes.md#overview)

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

# Data Types

JavaScript is not a strongly typed language in that you do not declare the type when the variable is created.  Its type is determined by what it is assigned an how it is used.  It contains three primitive types: number, string, and boolean, with everything else being an object.

* **number** - there is no distinction between real and integer type variables.  All numbers are represented by 64 bit floating point numbers.  It does allow integers to be stored with precision between -2^53 and 2^54.
* **strings** - strings in JavaScript are immutable, meaning they can't be changed, you can only create a new modified version of the string.  So JavaScript functions such as replace() do not change the original string, but instead must be assigned to a new string.
* **boolean** - binary (only two possible values) true/false, yes/no, on/off.  true/false are predefined and used to set and evaluate boolean.
* **object** - everything else is an Object.  JavaScript does include predefined objects such as **Date** (including Time) that include constructs for initializing and predefined methods and properties for working with them.  Another example would be the **RegExp** object for dealing with regular expressions.

Primitive types (number, string, and boolean) are value types and immutable, while objects are reference types and mutable

## Global Object

The global object contains the global defined properties and symbols available to all of the JavaScript program.  At the top most level, outside of all functions **this** will refer to the global object.  In the client side environment of the browser the **Windows** object will function as the global object.

The Global Object contains:

* Properties like undefined, NaN and Infinity
* Global functions like isNan(), parseInt(), and eval()
* Constructor functions for Date(), RegExp(), String(), Object(), Array()
* Global Objects like Math and JSON.
* Any global variables declared in the global scope will be stored here

## Wrapper Objects

Strings, numbers and booleans are primitive types and not objects.  However, they do have objects they are associated with String(), Number(), and Boolean() that they can be temporarily assigned to when access so that they can gain access to methods and properties to operate on these types.  This is all transparent and behind the scenes.  When the temporary object is no longer needed it is discarded.

## Type conversion

Type conversion happen dynamically depending on the context and don't normally require explicit cast/convert type operations

* "I'm string number " + 5 - 5 i converted to a string "5" and concatenated to "I'm string number 5"
* 5 + "10" - "10" is converted to the number 10 and added for a result of 15.

If an explicit conversion is needed for some reason it can be done with each primitives wrapper object function String(3) = "3", Boolean(0) = false, and Number("5") = 5.

## Variable Scope

Variables declared outside of all functions are global in scope.  Those variables defined within a function are local to that function, this includes any parameters passed into the function.  With ES5, which used **var** to declare variables there is no further distinction of scope within other blocks such as loops and conditionals, although the scope will be local within nested functions, and these nested functions have access to the variables declared in the function they are nested in.  With ES6, using **let** to declare a variable does allow the scope to be further limited to block of code it is declared in.

**Hoisting** - a variable declared within the local function scope does not have to appear before where it is used, it is considered "hoisted" to the top of the function where it will be available regardless of its position.

# String Formatting

## Formatring Numbers to String with Separators (commas)

From: [StackExchange](https://stackoverflow.com/questions/2901102/how-to-print-a-number-with-commas-as-thousands-separators-in-javascript)

Supported in all modern browsers
```js
var n = 34523453.345
n.toLocaleString()
"34,523,453.345"
```

It also works in Node.js as of v0.12 via inclusion of Intl

# Functions

Functions in JavaScript in a lot of ways behave like functions in other languages, but they do have some fairly unique characteristics such as function expressions (both named and unnamed), function constructors for creating objects, and self-invoking functions.  Part of the unique nature of JavaScript functions is the fact that they are actually objects and can be treated like other objects (they have methods, properties, etc and can be assigned to other objects and available)

## Standard functions

```JavaScript
function sum(x, y) {
  return x + y;
}

let total = sum(200, 550);
```

## Function expressions

```JavaScript
let func = function (str) {
    console.log('Hello, ' + str);
};

func('world');
```
Note the function variable (func in this case) can also be passed to other functions as parameters.

## Inline function expressions

The inline unnamed function `(item, pos)=>{` is using ES6 arrow function syntax, ES5 function(item, pos) {` syntax is also available

```JavaScript
// Get rid of duplicate entries in matches array
let uniqueMatches = matches.filter((item, pos)=>{
    return matches.indexOf(item)== pos; 
});
```

## Self-invoking function expressions

The following function will be invoked when the JavaScript file is loaded by the HTML page:

```JavaScript
(function () {
    console.log('Script loaded');
})();
```
Note the open parenthesis at the end is what makes this anonymous function expression self-invoking

## Object methods (using function expressions)

Uses ES6 arrow function syntax here, but the ES5 `fullname: function() {` syntax works as well.

```JavaScript
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

```JavaScript
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

# Event Handling

TODO: Fill in this section

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

```JavaScript
let form = document.getElementById("FormID");

 form.addEventListener("submit", (e) => {
      if ("Your Desired Conditions.") {
          e.preventDefault();
      }
 });
```

* Canceling the submit event with jQuery

```JavaScript
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
```JavaScript
let regEx = /exp/g
```

It can also be created with **new** using the RegExp constructor.  The second parameter is optional and provides flags ("g" = global, "m" = multi-line, "i" = ignore case)
```JavaScript
let regEx = new RegExp(/exp/, 'gm');
```
This method is useful when you want to combine multiple components (strings and other regular expressions).  For example,

```JavaScript
let wBound = /\b/;
let regEx = new RegExp(wBound.source + '^Test(ing|er|ed)$' + wBound.source, 'gm');
```
Using a string literal above but more typical a string variable, possibly from a web form.  Note the use of the **.source** property.  Without this it would not work correctly because the concatenates expression would double up the **/** delimiters.

### List of RegExp properties and methods

* **RegExp.exec(string)** - invoke to return a match within the string parameter based on the regexp regular expression.  It returns an array containing the results, or null if nothing found.  Element zero of the returned result is the matched text itself, while 1 thru n is the captured substrings if the RegEx search includes groups.  The array also contains the "index" for the beginning location of where the match was found.  If the global flag was set it will also include a .lastIndex property value where the next invocation of exec() will start when running it in a loop.  When the global flag is not set then exec() behaves like str.match().

  Example loop with exec() - You would use this if your expression includes a global (multi match) flag
  
  ```JavaScript
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
  
* **RegExp.source** - this property contains the text version of the regular expression without the **/** delimiters and flags.  Useful when concatenating multiple component pieces of the expression.  
* **RegExp.lastIndex** - when searching for multiple potential matches (with the "g" global flag) this will indicate where the next iteration of **RegExp.exec()** should start (in effect the end of the prior match + 1).  If you start searching a new string before the matches on the prior string are completed, then you need to set this property to zero to start over.  This is not necessary if the exec() loop completes (thus being set to null on its last iteration.
* **RegExp.global** - readonly property which is true if the global flag is set
* **RegExp.multiline** - readonly property which is true if multi-line flag set
* **RegExp.ignoreCase** - readonly property which is true if ignore case flag is set
* **RegExp.test(str)** - tests to see if the RegExp finds a match in str, if it does it returns true
* **RegExp.toString()** - convert the RegExp to a string

In addition to these RegExp properties and methods, you can use the **String.match(RegExp)** form.  This is similar to **RegExp.exec(str)** when the global flag is NOT set, otherwise use the exec() method instead.

## Converting text from the DOM into a RegExp object

```JavaScript
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
   Displays the Window object with a navigable tree of its subcomponents.

   ```
   document
   ```
   Displays the document object with a navigable tree of its subcomponents.

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
