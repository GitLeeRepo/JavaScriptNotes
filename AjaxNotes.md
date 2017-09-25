# Overview

Notes on the AJAX programming model

# References

* [W3 Schools](https://www.w3schools.com/js/js_ajax_intro.as) - AJAX Tutorial and Reference
* [AJAX Crash Course](https://www.youtube.com/watch?v=82hnvUYY6QA&list=PLillGF-RfqbYeckUaD1z6nviTp31GLTH8) - YouTube video by Traversey Media.  Many of the notes here come from this video.

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
        else {
            document.getElementById(outId).innerHTML =
                'Unable to load file, status = ' + this.status;
        }
    }
    xhr.send();
}
```
