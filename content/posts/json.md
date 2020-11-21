---
title: "JSON"
date: "2017-04-09T18:15:22+06:00"
---

## What is JSON?
JSON stands for JavaScript Object Notation. 

Douglas Crockford originally specified the JSON format in the early 2000s. Altohugh it derives from JavaScript, but as of 2017 many programming languages include code to generate and parse JSON-format data.

JSON filenames use the extension .json.

The official internet media type for JSON is 'application/json'

### Why use JSON?
Because It is

- lightweight data-interchange format. 
- language independent
- "self-describing" and easy to understand by both humans (to understand) and machines (to parse and generate).

### Areas of Usage?
JSON is heavily used in these areas : API, NoSQL, AJAX, Package Management (Composer, NPM, Bower etc)

### Why better than XML?
JSON is faster and easier than XML. It is parsed very easily into a ready-to-use JavaScript object while XML is much more difficult to parse.

---

## Data Structure & Rules
The JSON syntax is a subset of the JavaScript syntax.

### Data Structures

JSON is defined by two basic structures.

**1. A collection of name/value pairs.**

Different programming languages support this data structure in different names. Like object, record, struct, dictionary, hash table, keyed list, or associative array.

**e.g.,** `{ "name": "John", "age":  30, "member": false, "spouse": { "firstName": "Mary", "lastName": "Smith"} }`

**2. Ordered list of values.**

In various programming languages, it is called as array, vector, list, or sequence.
e.g., `["John","Mary","Peter","Sally"]`


### Syntax Rules
    
- Data is written as name/value pairs. `e.g., "name":"John"` (note : *JSON names require double quotes. JavaScript object names don't.*)
- Data is seperated by commas. e.g., `"name":"John", "age":30`
- Curly braces hold objects.

**e.g.,**

```json
{
  "name": "John",
  "age": 30,
  "member": false,
  "spouse": { //object
    "first_name": "Mary",
    "last_name": "Smith"
  }
}
```
- Square brackets hold arrays.

**e.g.,**

```json
{
    "name": "John",
    "age":  30,
    "member": false,
    "phoneNumbers": [ //array
        {
            "description": "home",
            "number": "123-456-7890"
        },
        {
            "description": "mobile",
            "number": "000-111-2222"
        }
    ]
}
```

### Data Types

Values must be one of the following data types.

- **a string** : sequence of zero or more Unicode characters. e.g., `{ "name":"John" }`
- **a number** : Integer, Fraction and Exponent. e.g., `{ "age":30 }`
- **an object (JSON object)** : starts and ends with '{' and '}'. a number of string value pairs can reside between. Keys must be strings, and values must be a valid JSON data type.

e.g.,

```json
{
    "employee":{ "name":"John", "age":30, "city":"New York" }
}
```
- **an array** : starts and ends with '[' and ']'. a number of values can reside between.

e.g.,

```json
{
    "employees":[ "John", "Anna", "Peter" ]
}
```
- **a boolean** : true or false. (TRUE or FALSE is not acceptable!). e.g., ```{ "accept":true }```
- **null** : null (NULL is not acceptable). e.g., ```{ "coupon":null }```


> note : JSON values cannot be a function, a date or undefined. (In JavaScript you can have these values)