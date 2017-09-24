# Overview

Notes on the JSON data exchange format

# References

* [W3 Schools](https://www.w3schools.com/js/js_json_intro.asp) - JSON Tutorial and Reference

* [JSON Crash Course](https://www.youtube.com/watch?v=wI1CWzNtE-M) - YouTube video by Traversey Media.  Many of the notes here come from this video.

# JSON Key Ideas

* JSON - JavaScript Object Notation

* Lightweight data interchange format

* Based on JavaScript Object Literals

* Often used with **AJAX**, essentially replacing XML

* Knowing JSON is key to working with **REST APIs**

# JSON Data Types

* Number - No destinction between float and integer. No quotes used

* String - Series of Unicode characters.  Must be in double quotes

* Boolean - True and False

* Arrays - Ordered List of items (strings, numbers, other arrays, objects) contained in square brackets

* Objects - Unordered Collection of **Key: Value** pairs. Can contain multiple tiers of embedded objects.  Enclosed in curly brackets.

* Null - Empty value.

# JSON Syntax

* Uses Key Value Pairs

`{ "key": "value" }`, for example `{ "name": "John" }`

* The **key** must be in double quotes, unlike JavaScript Literals in which the key normally isn't.  Whether **value** is in double quotes depends on the data type.

* Arrays are enclosed in square brackets

* Embedded objects are in curly brackets

* When in files it uses a **.json** file extension

* MIME Type is **"Application/json"**

# JSON Examples

## Example 1

```
{
	"first_name": "John",
	"last_name": "Doe",
	"age": 40,
	"gender": "male",
	"memberships": ["mem1", "mem2"],
	"address": {
			street: "1111 N 1st",
			city: "Boston",
			state: "MA"
		   },
	"balance": 99.99
}
``` 
Note the embedded arrays (membership) and objects (address)
