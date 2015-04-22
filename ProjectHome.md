# A fast and secure JSON parser in JavaScript #

This JSON parser does not attempt to validate the JSON, so may return a surprising result given a syntactically invalid input, but it does not use `eval` so is deterministic and is guaranteed not to modify any object other than its return value.


---


There are a number of JSON parsers in JavaScript at [json.org](http://json.org/).  This implementation should be used whenever security is a concern (when JSON may come from an untrusted source), speed is a concern, and erroring on malformed JSON is **not** a concern.

|                        | **Pros**                   | **Cons**                  |
|:-----------------------|:---------------------------|:--------------------------|
| This implementation    | Fast, secure             | Not validating          |
| `json_parse.js`    | Validating, secure       | Slow                    |
| `json2.js`         | Fast, some validation    | Potentially insecure    |

`json2.js` is very fast, but potentially insecure since it calls `eval` to
parse JSON data, so an attacker might be able to supply strange JS that looks like
JSON, but that executes arbitrary javascript.

If you do have to use `json2.js` with untrusted data, make sure you keep
your version of `json2.js` up to date so that you get patches as they're released.


---


To use, download http://json-sans-eval.googlecode.com/svn/trunk/src/json_sans_eval.js or download a minified version from the downloads tab and include it in your webpage.  Then you can call the global `jsonParse` function to parse JSON.  That function takes a string argument which must be valid JSON as defined in [RFC 4627](http://www.ietf.org/rfc/rfc4627.txt).


---


Once it is loaded, you can use parsed JSON as you would any other JavaScript object:
```
var myJson = '{ "x": "Hello, World!", "y": [1, 2, 3] }';
var myJsonObj = jsonParse(myJson);
alert(myJsonObj.x);  // alerts Hello, World!
for (var k in myJsonObj) {
  // alerts x=Hello, World!  and  y=1,2,3
  alert(k + '=' + myJsonObj[k]);
}
```


---


The `jsonParse` function takes an optional reviver function as specified at http://www.json.org/js.html so it should behave identically to the `JSON.parse` specified in the EcmaScript 5 draft.