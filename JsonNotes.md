# Overview

Notes on the JSON data exchange format

# References

* [W3 Schools](https://www.w3schools.com/js/js_json_intro.asp) - JSON Tutorial and Reference
* [JSON Crash Course](https://www.youtube.com/watch?v=wI1CWzNtE-M) - YouTube video by Traversy Media.  Many of the notes here come from this video.

## My Other Notes

* [JavaScriptNotes](https://github.com/GitLeeRepo/JavaScriptNotes/blob/master/JavaScriptNotes.md#overview)

# JSON Key Ideas

* JSON - JavaScript Object Notation
* Lightweight data interchange format
* Based on JavaScript Object Literals
* Often used with **AJAX**, essentially replacing XML
* Knowing JSON is key to working with **REST APIs**

# JSON Data Types

* Number - No distinction between float and integer. No quotes used
* String - Series of Unicode characters.  Must be in double quotes
* Boolean - True and False
* Arrays - Ordered List of items (strings, numbers, other arrays, objects) contained in square brackets
* Objects - Unordered Collection of **Key: Value** pairs. Can contain multiple tiers of embedded objects.  Enclosed in curly brackets.
* Null - Empty value.

# JSON Syntax

* Uses Key Value Pairs

	```
	{ "key": "value" }`, for example `{ "name": "John" }
	```

* The **key** must be in double quotes, unlike JavaScript Literals in which the key normally isn't.  Whether **value** is in double quotes depends on the data type.

* Arrays are enclosed in square brackets

* Embedded objects are in curly brackets

* When in files it uses a **.json** file extension

* MIME Type is **"Application/json"**

* Note JSON cannot contain embedded functions like a JavaScript function can

* You can check if your JSON is valid at [https://jsonlint.com/](https://jsonlint.com/)

# JSON Examples

## Example 1 - JSON with embedded arrays and objects

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

## Example 2 - Converting between JSON and JavaScript objects

* To use JavaScript to convert back and forth between JSON and JavaScript objects:

	```
	<script>
		var person = {
			name: "John Doe",
			age: 44
		}

		// note at this point person is a valid object: person.name is a legal reference

		// to convert JavaScript object to JSON - will add the double quotes to the key
		person = JSON.stringify(person);

		// note the above person can no longer be used as an object: person.name would be undefined

		// to convert back to JavaScript from JSON - will make it a valid JavaScript Object again
		person = JSON.parse(person);

		// now person is a valid object: person.name is a legal again	
	</script>
	```

# PHP Example Returning JSON

* Returning JSON from a MySQL query

	```php
	$query = 'SELECT * FROM users';
	$result = mysqli_query($conn, $query));

	$users = mysqli_fetch_all($result, MYSQLI_ASSOC);

	// convert $users associative array to JSON
	echo json_encode($users);
	```
