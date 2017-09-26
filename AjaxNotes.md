# Overview

Notes on the AJAX programming model

# References

* [W3 Schools](https://www.w3schools.com/js/js_ajax_intro.as) - AJAX Tutorial and Reference
* [AJAX Crash Course](https://www.youtube.com/watch?v=82hnvUYY6QA&list=PLillGF-RfqbYeckUaD1z6nviTp31GLTH8) - YouTube video by Traversy Media.  Many of the notes here come from this video.

# What is AJAX

* Stands for Asynchronous JavaScript and XML (JSON is used now more that XML)

* Used to send data asynchronously

* Used to update web pages with data without having to refresh then entire page

* Used with REST APIs which generally return JSON

* Uses XmlHttpRequest() function in JavaScript to make the request which creates an object that can then process the response

* In addition to XmlHttpRequest, there are other libararies with methods for making AJAX calls.  Examples include, jQuery, Axios, Superagent, Fetch API, Prototype, Node HTTP.

# XmlHttpRequest (XHR) Object in JavaScript

* An API in the form of an object

* Provided by the browsers JavaScript environment

* Provides methods for transferring data between the client and the server

* Can be used with protocols other than HTTP

* Can be used with data other than XML (JSON, text files, etc)

# Old vs New way of processing the response

* Old way with onReadyStateChange

```javascript
var xhr = new XMLHttpRequest();

xhr.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
        document.getElementById("output").innerHTML = xhr.responseText;
    }
}
```

Note with this method you must check the readyState in addition to the status

* New way with onload

```javascript
var xhr = new XMLHttpRequest();

xhr.onload = function () {
    if (this.status == 200) {
        document.getElementById("output").innerHTML = xhr.responseText;
    }
}
```

Note here you don't need to check readyState since onload is only triggered when the readyState is 4.

# Additional XHR methods and properties

## onprogress

```javascript
xhr.onprogress = function () {
    console.log("In onprogress");
}
```
You can use this if you want to display a progress indicator

## onerror

```javascript
xhr.onerror = function () {
    console.log("Error Occurred");
}
```
Use with onload to handle any errors in processing the request

# Examples

# Ex 1 - Get and display text file

* Update the div section with contents of text file

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax 1</title>
</head>
<body>
    <button id="button">Get Text file</button>

    <div id="output" style="margin-top:30px" ></div>

    <script>
        document.getElementById("button").addEventListener("click", loadText);

        function loadText() {
            var xhr = new XMLHttpRequest();

            xhr.onload = function () {
                if (this.status == 200) {
                    document.getElementById("output").innerHTML = xhr.responseText;
                }
                else {
                    document.getElementById("output").innerHTML =
                        'Unable to load file, status = ' + this.status;
                }
            }
            xhr.open("GET", "test.txt");
            xhr.send();
        }
    </script>
</body>
</html>
```

## Ex2 - Get JSON user data

* Get JSON data from the json\users.json file

```javascript
function loadUsers(outId) {
    var xhr = new XMLHttpRequest();

    xhr.open('GET', 'json/users.json');
    xhr.onload = function () {
        if (this.status == 200) {
            var users = JSON.parse(this.responseText);
            document.getElementById(outId).innerHTM = '';
            for (i in users) {
                document.getElementById(outId).innerHTML +=
                    users[i].name + ' is ' + users[i].age + ' and lives in ' + users[i].city + '<br>';
            }
        }
    }
    xhr.send();
}
```
Note the use of the JSON.parse() method.  This is needed to convert the JSON data into a JavaScript object, so its individual properties can be accessed.

## Ex3 - Getting JSON from an external API

* Using the GitHub API to get user data

```javascript
function loadGitHubUsers(outId) {
    var xhr = new XMLHttpRequest();

    xhr.open('GET', 'https://api.github.com/users');
    xhr.onload = function () {
        if (this.status == 200) {
            var users = JSON.parse(this.responseText);
            document.getElementById(outId).innerHTM = '';
            for (var i = 0; i < 5; i++) {
                document.getElementById(outId).innerHTML +=
                    '<img src="' + users[i].avatar_url + '" width="70" height="70">' +
                    ' id: ' + users[i].id +
                    ' login: ' + users[i].login + '<br>';
            }
        }
    }
    xhr.send();
}
```
Note: For security reasons browser place a restriction limiting requests to the current server. But if the external site complies with the proper criteria helping to ensure safe access, such as using CORS (Cross Origin Resource Sharing) specification external site data can be accessed.  This is typically what is done on sites that provide a web API.

## Ex 4 - Using parameters when using XMLHttpRequest's open method

* Making a request from a PHP server side script

```
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'getUserInfo.php?name=Bill');
```
Note: this is the same way of providing a GET parameter with a form request to a PHP script, but in the case of using AJAX methods (XMLHttpRequest) the entire page does not need to be refreshed.

# Ex 5 - Using an HTML form to submit an AJAX request

As long as you take steps to prevent the page reload you can use a form to submit an AJAX request

* Example calling a PHP script using the forms text field to provide a parameter:

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax with Form</title>
</head>
<body>
    <form id="getForm">
        <input type="text" name="name" id="name1">
        <input type="submit" value = "Submit">
    </form>
    <br><br>
    <div id="out"></div>

<script>
    document.getElementById("getForm").addEventListener("submit", getName);

    function getName(e) {
        //Prevent default action, in this case:
        //Prevent a submit button from submitting a form
        e.preventDefault();

        var name = document.getElementById("name1").value;

        var xhr = new XMLHttpRequest();
        xhr.open("GET", "process.php?name="+name);  // with GET params go here

        xhr.onload = function () {
            if (this.status == 200) {
                document.getElementById("out").innerHTML = this.responseText;
            }
        }
        xhr.send();
    }
</script>
</body>
</html>
```

Note: to prevent the reload of the page e.preventDefault() is used in the event handler

## Ex 6 - Using POST instead of GET

This is the same as the prior example, but it uses POST instead of GET.  Notice how POST require slightly more code to handle the parameters than GET does.

* POST Example:

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Ajax with Form</title>
</head>
<body>
    <form id="postForm">
        <input type="text" name="name" id="name2">
        <input type="submit" value = "Submit">
    </form>
    <br><br>
    <div id="out"></div>

<script>
    document.getElementById("postForm").addEventListener("submit", postName);

    function postName(e) {
        //Prevent default action, in this case:
        //Prevent a submit button from submitting a form
        e.preventDefault();

        var name = document.getElementById("name2").value;
        var params = "name="+name;

        var xhr = new XMLHttpRequest();
        xhr.open("POST", "process.php");  // with POST no params here
        xhr.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

        xhr.onload = function () {
            if (this.status == 200) {
                document.getElementById("out").innerHTML = this.responseText;
            }
        }
        xhr.send(params);  // with POST we send the params here
    }
</script>    
</body>
</html>
```
Note: In addition to slightly more code to handle the parameters, post also includes the xhr.setRequestHeader() method to set the content type.
