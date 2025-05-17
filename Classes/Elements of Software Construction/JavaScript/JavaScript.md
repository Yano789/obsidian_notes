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
    <script src="textandbutton.js"></script>
    <meta charset="utf-8" />
    <title>50.003 sample code: Text and Button</title>
  </head>
  <body>
    <div>Your input: <input id="textbox1" type="text" /></div>
    <div>Output: <span id="span1"></span></div>
    <div><button id="button1">Submit</button></div>
  </body>
</html>
```


## Variables
2 ways to declare variables:
1. **var** - *global* scope/variable *in a function*
2. **let** - block/*local* scope *in a block ONLY*
3. **const** - declares *constant*

![[JavaScript-1.webp]]

## Function and Anonymous Function
**Function**:
