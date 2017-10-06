# Overview

Notes on ESlint for JavaScript (including Node.js, React, JQuery, etc)

# References

* [Main site](https://eslint.org/)

# Installation

The ESLint installation uses **NPM** (Node Package Module) therefore, Node.js must be installed.  The notes here are for setting it up globally, it can also be installed per project if desired.

Note: Since ESLint is installed globally here, any subsequent installation of ESLint related plugins should also be installed globally in order for them to work properly.

Run:
```
npm install -g eslint
```

To initialize and customize the .eslintrc file in a project folder run:

```
eslint --init
```

This will ask you questions on your coding style and environment, whether you are using Node.js and ES6 features for example.  This creates the .eslintrc file in your project root.  This file can be copied to other projects, in which case you don't need to run `eslint --init` for them.  You can also copy to a subfolder in your project if you want to apply different rules for different sets of code.

To run ESLint outside of an editor that is configured to use it, you can run it from the command line, for example:

```
eslint myCode.js
```

# Editor/IDE Usage

## Visual Studio Code

ESLint is available in VS Code through an extension.  My extension was installed when I clicked on "JavaScript" under "Customize" on the Welcome page (at least I don't think it was there before).  It gave me errors saying ESLint needed to be installed, in which case I ran the NPM install as outlined above.  It continued to warn me about other related plugins that it needed, which I also installed globally with NPM.  Unfortunately, I did not take detailed notes at the time to note which additional modules it needed (it was two or three).  Once completed, it has run without issue since then, integrating well with VS Code.

## Visual Studio 2017 IDE

Apparently it is installed by default with VS 2017 and just needs to be enabled.  Mine had it, so not sure if it was installed with JavaScript related install options or not (such as Node.js).  I enabled it by doing the following

* Open the **Tools** menu and select **Options**
* Navigate to **Text Editor/JavaScript-TypeScript/ESLint**
* Set **Enabled** to True

I found it was using the "C:\\Users\\UserName\\.eslintrc" (no .json extension) file for its configuration.  I tried adding a local .eslintrc.json file to the projects JavaScript folder and it caused ESLint to stop working (no errors, it just nolonger worked reporting obvious issue).  It may have to do with the default one using numbers for values instead of strings, the local .eslintrc.json files use string values, altough they accept the number eqivellent also (e.g. 0 for "off", 1 for "warn", 2 for "error").  I tried adding the string value syntax to the "C:\\Users\\UserName\\.eslintrc" version with the same result, ESLint stopped working.  I will investigate this further at a later time.

# .eslintrc.json file

Contains the configuration settings for ESLint.  It is placed or generated in your projects folder.  Refer to the "Instalation" section for details on generating one. An existing one can also be compied from another project.

Example .eslint.json file:

```json
{
    "env": {
        "browser": true,
        "es6": true,
        "node": true,
        "jquery": true
    },
    "extends": "eslint:recommended",
    "parserOptions": {
        "sourceType": "module"
    },
    "rules": {
        "indent": [
            "warn",
            4
        ],
        "linebreak-style": [
            "error",
            "windows"
        ],
        "quotes": [
            "warn",
            "single"
        ],
        "semi": [
            "error",
            "always"
        ],
        "no-console": "off",
        "no-var": "warn",
        "no-unused-vars": "warn",
        "prefer-arrow-callback":"warn"
    }
}
```

# Issues

## Issue: ESLint flags global functions as unused-vars

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

## Issue with Visual Studio 2017 .eslintrc file

Refer to the "Visual Studio 2017 IDE" section above for details
