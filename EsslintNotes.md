# Overview

Notes on eslint

# References

* [Main site](https://eslint.org/)

# Installation



# Issues

## Eslint flags global functions as unused

For web pages that call JavaScript functions in a separate .js file, the functions in that .js file will be flagged as unused if you have warn or error defined for the **no-unused-vars** rule.  This is unfortunate because this rule is desireable in general for variables (function names are treated as variable in JavaScript), but not for these functions it doesn't make sense in this environment. Exported functions will not trigger this, but this is more of a server side (Node.js) technique and not done for client side web page scripting.  Below is the only reasonable way I have found so far to deal with this, but I rather not have to add this clutter to the code, and more importantly it may miss arguements that are unused that you want to identify.

* To disable on a per function level

  Add this comment to the function declaration line
  
  ```javascript
  function myFunc() { // eslint-disable-line no-unused-vars
  ```
  
  An alternative is the following, but this is undesireable in that it redefines the rule everytime it is used (once for each function)
  
  ```javascript
   /*eslint no-unused-vars: ["warn", {"vars": "all", "varsIgnorePattern": "myFunc"}]*/
   function myFunc() {
   ...
  ```
