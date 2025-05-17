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
