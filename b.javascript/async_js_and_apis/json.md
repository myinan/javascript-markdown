# JSON
 JSON is a lightweight data interchange format that is easy for humans to read and write, and easy for machines to parse and generate. JavaScript Object Notation (JSON) is a standard text-based format for representing structured data based on JavaScript object syntax. It is often used to transmit data between a server and a web application, as well as for configuration files and data storage.

JSON is a text-based data format following JavaScript object syntax, which was popularized by Douglas Crockford. Even though it closely resembles JavaScript object literal syntax, it can be used independently from JavaScript, and many programming environments feature the ability to read (parse) and generate JSON.

JSON exists as a string — useful when you want to transmit data across a network. It needs to be converted to a native JavaScript object when you want to access the data. This is not a big issue — JavaScript provides a global `JSON` object that has methods available for converting between the two.

Note: Converting a string to a native object is called *deserialization*, while converting a native object to a string so it can be transmitted across the network is called *serialization*.

A JSON string can be stored in its own file, which is basically just a text file with an extension of .json, and a MIME type of application/json.

### JSON Structure
As described above, JSON is a string whose format very much resembles JavaScript object literal format. You can include the same basic data types inside JSON as you can in a standard JavaScript object — strings, numbers, arrays, booleans, and other object literals. This allows you to construct a data hierarchy, like so:

```json
// .json
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}

```

If we loaded this string into a JavaScript program and parsed it into a variable called superHeroes for example, we could then access the data inside it using the dot/bracket notation of the object syntax of Javascript.

```js
// .js
superHeroes.homeTown;
superHeroes["active"];
```

To access data further down the hierarchy, you have to chain the required property names and array indexes together. For example, to access the third superpower of the second hero listed in the members list, you'd do this:

```js
// .js
superHeroes["members"][1]["powers"][2];
```

### Arrays as JSON
Above we mentioned that JSON text basically looks like a JavaScript object inside a string. We can also convert arrays to/from JSON. Below is also valid JSON, for example:

```json
[
  {
    "name": "Molecule Man",
    "age": 29,
    "secretIdentity": "Dan Jukes",
    "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
  },
  {
    "name": "Madame Uppercut",
    "age": 39,
    "secretIdentity": "Jane Wilson",
    "powers": [
      "Million tonne punch",
      "Damage resistance",
      "Superhuman reflexes"
    ]
  }
]
```

The above is perfectly valid JSON. You'd just have to access array items (in its parsed version) by starting with an array index, for example `[0]["powers"][0]`.

### Some notes regarding JSON
+ JSON is purely a string with a specified data format — it contains only properties, no methods.

+ JSON requires double quotes to be used around strings and property names. Single quotes are not valid other than surrounding the entire JSON string.

+ Even a single misplaced comma or colon can cause a JSON file to go wrong, and not work. You should be careful to validate any data you are attempting to use (although computer-generated JSON is less likely to include errors, as long as the generator program is working correctly). You can validate JSON using an application like JSONLint.

+ JSON can actually take the form of any data type that is valid for inclusion inside JSON, not just arrays or objects. So for example, a single string or number would be valid JSON.

+ Unlike in JavaScript code in which object properties may be unquoted, in JSON only quoted strings may be used as properties.

### Built-in JSON object of Javascript
In JavaScript, the built-in JSON object is used for working with JSON (JavaScript Object Notation) data.

The JSON object in JavaScript provides two methods:

1. **`JSON.stringify()`**: This method is used to convert a JavaScript object into a JSON string. It takes an object as a parameter and returns a string representation of that object in JSON format.

   ```javascript
   const myObject = { name: "John", age: 30, city: "New York" };
   const jsonString = JSON.stringify(myObject);
   console.log(jsonString);
   // Output: {"name":"John","age":30,"city":"New York"}
   ```

    When storing data, the data has to be in a certain format, and regardless of where you choose to store it, text is always one of the legal formats.

    JSON makes it possible to store JavaScript objects as text.

    ```js
    // Storing data in local storage

    // Storing data:
    const myObj = {name: "John", age: 31, city: "New York"};
    const myJSON = JSON.stringify(myObj);
    localStorage.setItem("testJSON", myJSON);

    // Retrieving data:
    let text = localStorage.getItem("testJSON");
    let obj = JSON.parse(text);
    document.getElementById("demo").innerHTML = obj.name;
    ```

    In JSON, date objects are not allowed. The JSON.stringify() function will convert any dates into strings.

    ```js
    const obj = {name: "John", today: new Date(), city : "New York"};
    const myJSON = JSON.stringify(obj); // {"name":"John","today":"2024-01-02T17:42:36.257Z","city":"New York"}
    ```

    In JSON, functions are not allowed as object values. The JSON.stringify() function will remove any functions from a JavaScript object, both the key and the value:

    ```js
    const obj = {name: "John", age: function () {return 30;}, city: "New York"};
    const myJSON = JSON.stringify(obj); // {"name":"John","city":"New York"}
    ```

    This can be omitted if you convert your functions into strings before running the JSON.stringify() function.

    ```js
    const obj = {name: "John", age: function () {return 30;}, city: "New York"};
    obj.age = obj.age.toString();
    const myJSON = JSON.stringify(obj); // {"name":"John","age":"function () {return 30;}","city":"New York"}
    ```

    **Important: If you send functions using JSON, the functions will lose their scope, and the receiver would have to use eval() to convert them back into functions.**


2. **`JSON.parse()`**: This method is used to parse a JSON string and convert it into a JavaScript object. It takes a JSON-formatted string as a parameter and returns the corresponding JavaScript object.

   ```javascript
   const jsonString = '{"name":"John","age":30,"city":"New York"}';
   const parsedObject = JSON.parse(jsonString);
   console.log(parsedObject);
   // Output: { name: 'John', age: 30, city: 'New York' }
   ```

   When using the JSON.parse() on a JSON derived from an array, the method will return a JavaScript array, instead of a JavaScript object.

   ```js
   const text = '["Ford", "BMW", "Audi", "Fiat"]';
   const myArr = JSON.parse(text);
   document.getElementById("demo").innerHTML = myArr[0]; // Ford
   ```

    Date objects are not allowed in JSON. If a date is written as string in the JSON file, you can convert it back into a date object.

    ```js
    const text = '{"name":"John", "birth":"1986-12-14", "city":"New York"}';
    const obj = JSON.parse(text);
    obj.birth = new Date(obj.birth);

    document.getElementById("demo").innerHTML = obj.name + ", " + obj.birth;
    // John, Sun Dec 14 1986 02:00:00 GMT+0200 (GMT+03:00) (Current date)
    ```

    Functions are not allowed in JSON. If a function is included in the JSON as a string, you can convert it back into a function.

    ```js
    const text = '{"name":"John", "age":"function () {return 30;}", "city":"New York"}';
    const obj = JSON.parse(text);
    obj.age = eval("(" + obj.age + ")");

    document.getElementById("demo").innerHTML = obj.name + ", " + obj.age(); // John, 30
    ```

    **Important: You should avoid using functions in JSON, the functions will lose their scope, and you would have to use eval() to convert them back into functions.**

   It's important to note that the JSON string passed to `JSON.parse()` must be valid JSON, or it will throw a syntax error.

These methods make it easy to work with JSON data in JavaScript, allowing you to convert between JavaScript objects and JSON strings, facilitating data interchange in web applications.

### Functions/methods can't be stored in JSON format
JSON, even though it uses a syntax close to Javascript objects, is designed as a language independent data serialization format. So only the "basic types" are supported by JSON, which are:
+ Number (integer, real, or floating point)
+ String (double-quoted Unicode with backslash escaping)
+ Boolean (true and false)
+ Array (an ordered sequence of values, comma-separated and enclosed in square brackets)
+ Object (collection of key:value pairs, comma-separated and enclosed in curly braces)
+ null

Functions/methods, which are executable code, cannot be directly stored in JSON format due to its limited support for basic data types.

Of course, storing arguments and the body of a function as string in JSON is always possible:

```json
{"function":{"arguments":"a,b,c","body":"return a*b+c;"}}
```

Now parse json and instantiate the function:

```js
var f = new Function(function.arguments, function.body);
```

But using JSON this way is not recommended for three main reasons:
1. When using the Function constructor to create a function from a string, the created function will not capture the lexical scope of its surroundings.
2. If the source of the string is not trusted, it can be used to inject malicious code into the script.
3. Since JSON is designed as a language independent data serialization format, storing Javascript spesific data in a .json file is discouraged.

In summary, while it's technically possible to store function information in JSON and recreate functions using the Function constructor, it's not recommended due to potential security risks and limitations.

**Note:** Mis-formatted JSON is a common cause of errors. This [JSON formatter website](https://jsonformatter.curiousconcept.com/) lets you paste in JSON code and will search it for formatting errors.