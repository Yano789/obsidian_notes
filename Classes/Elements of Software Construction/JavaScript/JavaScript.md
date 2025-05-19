---
tags:
  - review
aliases:
  - JS
---
a language designed to run in the browser to handle user interaction with document components

## Simple Example

This is an [[HTML (Hyper Text Markup Language)|HTML]] document that contains a *script* element.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>50.003</title>
    <link rel="stylesheet" href="hello.css" />
    <script src="hello.js"></script>
  </head>
  <body>
    <p class="heading">Welcome to 50.003!</p>
    <p id="msg1" class="message">It's about Software Engineering!</p>
  </body>
</html>
```

Inside *hello.js* is:

```javascript
console.log("hello");
```

This will output the *hello* message in the console. If we want the message to output as a **pop-up window**, we can use **alert()**

```javascript
var msg = "hello";
// console.log(msg);
alert(msg);
```

## Input/Output
```html
<!DOCTYPE html>
<html>
  <head>
    <script src="textandbutton.js"></script> <!--javascript for input/output-->
    <meta charset="utf-8" />
    <title>50.003 sample code: Text and Button</title>
  </head>
  <body>
    <div>Your input: <input id="textbox1" type="text" /></div> <!--Input-->
    <div>Output: <span id="span1"></span></div> <!--Span is for output space-->
    <div><button id="button1">Submit</button></div> <!--button to press-->
  </body>
</html>
```

Inside *textandbutton.js*:
```javascript
function handleButton1Click() {
  var textbox1 = document.getElementById("textbox1");
  var span1 = document.getElementById("span1");
  span1.innerHTML = textbox1.value;
}

function run() {
  var button1 = document.getElementById("button1");
  button1.addEventListener("click", handleButton1Click);
}

document.addEventListener("DOMContentLoaded", run);
```

*NOTE: REVIEW AFTER LECTURE*

## Variables
2 ways to declare variables:
1. **var** - *global* scope/variable *in a function*
2. **let** - block/*local* scope *in a block ONLY*
3. **const** - declares *constant*

```javascript
var varA = "varA"; // Global Scope
let letA = "letA"; // Global Scope

function globalAccess() {
  console.log(varA); // Accessible anywhere
  console.log(letA); // Accessible anywhere
}
globalAccess();

function outerFunc() {
  if (1 < 2) {
    // Curly bracket defines a block
    var varB = "varB"; // Function Scope
    let letB = "letB"; // Block Scope
  }
  console.log(varB); // varB is accessible
  console.log(letB); // Error, letB is NOT accessible
}
outerFunc();
```

## Function and Anonymous Function
The syntax of a [[Function]]:
```javascript
function functionName(parameters) {
  // function body
  return output;
}

// Invoke function
functionName(args);
```

An **Anonymous Function** is a function that is meant to be used only once:

Without *Function Name*
```javascript
function (params) {
  //function body
  return output;
}
```

or

Without *Function Name* and *Function Declaration*
```javascript
(params) => {
  //function body
  return output;
};
```

## Basic Data Structures
### String

**Initialising a String**
```javascript
var myStr = "hello";
```

**Accessing characters**
```javascript
myStr[0]; // returns first characters
myStr[myStr.length - 1]; // returns last character
var newStr = myStr + " 123"; // returns hello 123
myStr.concat(" 123"); //produces the same thing (hello 123)
```

Embed a *String* into a **Template String**
```javascript
var newStr = `${myStr} 123`; // we use `` instead of "" to make multiline
```

*Note: we DONT use "" so that we can make the strings multi line*

**Splitting a String**
```javascript
var myStrs = newStr.split(" "); //splits into an array: ["hello", "123"]
var myChars = newStr.split (""); // ["h","e","l", ...]
var notSplitted = newStr.split(); // return ["hello 123"]
```

**Extracting Sub-string**
```javascript
myStr.substring(1,3); // "el" (starting index, ending index excluded)
myStr.substr(1,2); // "el" (starting index, length of the substring)
myStr.slice(1,3); // "el" works the same as substring but can also be used to access characters if only one argument (myStr.slice(2)==myStr[2])
```

`.slice()` can also accept negative integers

```javascript
myStr.slice(-3); // "llo"
myStr.slide(-3,-1); // "ll"
```

### Array
**Initialising an Array**
```javascript
var myArr = ["a","b","c"];
```

**Access Element in Array**
```javascript
myArr[0]; // "a"
```

**Slicing Array**
```javascript
myArr.slice(1,3); // Array["b","c"]
```

**Reverse**
```javascript
myArr.reverse(); 
myArr; // Array["c","b","a"]
```

**Concat** 
```javascript
myArr.concat(["d"]); // Array["a","b","c","d"]
```

*Note: (+) does not concat* $\rightarrow$ `myArr + ["d"]; // 'a,b,cd`'

**Joining and Array**
```javascript
myArr.join(","); // 'a,b,c'
```

**Push and Pop**
```javascript
myArr.push("d");
myArr; // Array["a,"b","c","d"]

myArr.pop();
myArr; // Array["a","b","c"]
```

**Unshift (insert element at the beginning)**
```javascript
myArr.unshift("d");
myArr; // Array["d","a","b","c"]
```

*Note: Unshift can insert more than one element* $\rightarrow$ `myArr.unshift(e1, e2, ...)` 

**Splice (Specific Insert/Delete)**
```javascript
myArr.splice(1,0,"z"); // (index to insert at, how many elements to remove after index, element)
myArr; // Array["a","z","b","c"]

myArr.splice(1,1);
myArr; // Array["a","b","c"]
```

### Object (Dictionary)
```javascript
var myObj = { apple: 100, orange: 50 };
myObj["apple"]; // 100

myObj["durian"] = 200;
myObj; // { 'apple': 100, 'orange': 50, 'durian': 200 }

myObj[1] = 1000; // using integers as keys
myObj[1]; // 1000
```

**Dot Operator (Access Values Another Way)**
```javascript
myObj.apple; // 100
```

*Note: You cannot use the dot operator on INTEGER KEYS*

**Delete (Remove Key)**
```javascript
delete myObj[1];
myObj; // { 'apple': 100, 'orange': 50, 'durian': 200 }
```

**Object.keys and Object.entries**
```javascript
Object.keys(myObj); // ['apple', 'orange', 'durian', 1]
Object.entries(myObj); // [['apple', 100], ['orange', 50], ['durian', 200], [1, 1000]]
```

## Control Flow Statements

### if-else
```javascript
var apple_count = null;
if ("apple" in myObj) {
  apple_count = myObj.apple;
} else {
  apple_count = 0;
}
```

### for
```javascript
var sum = 0;
var kvs = Object.entries(myObj);
for (let i = 0; i < kvs.length; i++) {
  sum = sum + kvs[i][1];
}
sum; // 350
```

**for-in and for-of**
```javascript
for (let i in kvs) { // goes through indeces of kvs
  sum = sum + kvs[i][1];
}

for (let kv of kvs) { // goes through elemnts in kvs
  sum = sum + kv[1];
}
```

### while
```javascript
var i = 0;
while (i < kvs.length) {
  sum = sum + kvs[i][1];
  i++;
}
```

### forEach and map
```javascript
kvs.forEach(function (kv) { // apply function (kv) 
  sum = sum + kv[1];
});
```
