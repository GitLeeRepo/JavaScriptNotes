# Overview

JavaScript notes, particularly as it applies to browsers

# Chrome Tools

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

