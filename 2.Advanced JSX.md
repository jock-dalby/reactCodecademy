---- class vs ClassName ------

In HTML, it's common to use class as an attribute name:
```javascript
<h1 class="big">Hey</h1>
```
In JSX, you can't use the word class! You have to use className instead:
```javascript
<h1 className="big">Hey</h1>
```
This is because JSX gets translated into JavaScript, and class is a reserved word in JavaScript.

When JSX is rendered, JSX className attributes are automatically rendered as class attributes.

```javascript
var React = require('react');
var ReactDOM = require('react-dom');

// Write code here:
var myDiv = (
	<div className="big">
    I AM A BIG DIV
  </div>
)

ReactDOM.render(myDiv, document.getElementById('app'));
```

---- Self-closing Tags ------

Most HTML elements use two tags: an opening tag (<div>), and a closing tag (</div>). However, some HTML elements such as <img> and <input> use only one tag. The tag that belongs to a single-tag element isn't an opening tag nor a closing tag; it's a self-closing tag.

When you write a self-closing tag in HTML, it is optional to include a forward-slash immediately before the final angle-bracket:

```javascript
Fine in HTML with a slash:

  <br />

Also fine, without the slash:

  <br>
```
But!

In JSX, you have to include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error:
```javascript
Fine in JSX:

  <br />

NOT FINE AT ALL in JSX:

  <br>
```
---- Curly Braces in JSX ------

Any code in between the tags of a JSX element will be read as JSX, not as regular JavaScript! JSX doesn't add numbers - it reads them as text, just like HTML.

You need a way to write code that says, "Even though I am located in between JSX tags, treat me like ordinary JavaScript and not like JSX."

You can do this by wrapping your code in curly braces.
```javascript
var React = require('react');
var ReactDOM = require('react-dom');

// Write code here:
ReactDOM.render(
  <h1>{2 + 3}</h1>,
  document.getElementById('app')
);
```
---- Variables in JSX ------

When you inject JavaScript into JSX, that JavaScript is part of the same environment as the rest of the JavaScript in your file.

That means that you can access variables while inside of a JSX expression, even if those variables were declared on the outside.

```javascript
// Declare a variable:
var name = 'Gerdo';

// Access your variable
// from inside of a JSX expression:
var greeting = <p>Hello, {name}!</p>;
```

```javascript
var React = require('react');
var ReactDOM = require('react-dom');

var theBestString = 'tralalalala i am da best';

ReactDOM.render(<h1>{theBestString}</h1>, document.getElementById('app'));
```
---- Variable Attributes in JSX ------

When writing JSX, it's common to use variables to set attributes.

Here's an example of how that might work:
```javascript
// Use a variable to set the `height` and `width` attributes:

var sideLength = "200px";

var panda = (
  <img
    src="images/panda.jpg"
    alt="panda"
    height={sideLength}
    width={sideLength} />
);
```
Notice how in this example, the img's attributes each get their own line. This can make your code more readable if you have a lot of attributes on one element.

Object properties are also often used to set attributes:

```javascript
var pics = {
  panda: "http://bit.ly/1Tqltv5",
  owl: "http://bit.ly/1XGtkM3",
  owlCat: "http://bit.ly/1Upbczi"
};

var panda = (
  <img
    src={pics.panda}
    alt="Lazy Panda" />
);

var owl = (
  <img
    src={pics.owl}
    alt="Unimpressed Owl" />
);

var owlCat = (
  <img
    src={pics.owlCat}
    alt="Ghastly Abomination" />
);
```
---- Event Listeners in JSX ------

JSX elements can have event listeners, just like HTML elements can. Programming in React means constantly working with event listeners.

You create an event listener by giving a JSX element a special attribute. Here's an example:
```javascript
<img onClick={myFunc} />
```
An event listener attribute's name should be something like onClick or onMouseOver: the word on, plus the type of event that you're listening for.

An event listener attribute's value should be a function. The above example would only work if myFunc were a valid function that had been defined elsewhere:
```javascript
function myFunc () {
  alert('Make myFunc the pFunc... omg that was horrible i am so sorry');
}

<img onClick={myFunc} />
```
Note that in HTML, event listener names are written in all lowercase, such as onclick or onmouseover. In JSX, event listener names are written in camelCase, such as onClick or onMouseOver.
