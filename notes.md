**** REACT ****

React.js is a JavaScript library. It was developed by engineers at Facebook.

Here are just a few of the reasons why people choose to program with React:

- React is fast. Apps made in React can handle complex updates and still feel quick and responsive.

- React is modular. Instead of writing large, dense files of code, you can write many smaller, reusable files. React's modularity can be a beautiful solution to JavaScript's maintainability problems.

- React is scalable. Large programs that display a lot of changing data are where React performs best.

- React is flexible. You can use React for interesting projects that have nothing to do with making a web app. People are still figuring out React's potential. There's room to explore.

- React is popular. While this reason has admittedly little to do with React's quality, the truth is that understanding React will make you more employable.


**** JSX ****

JSX is a syntax extension for JavaScript. It was written to be used with React. JSX code looks a lot like HTML.

What does "syntax extension" mean?

In this case, it means that JSX is not valid JavaScript. Web browsers can't read it!

If a JavaScript file contains JSX code, then that file will have to be compiled. That means that before the file reaches a web browser, a JSX compiler will translate any JSX into regular JavaScript.

Codecademy's servers already have a JSX compiler installed, so you don't have to worry about that for now. Eventually we'll walk through how to set up a JSX compiler on your personal computer.

---- JSX Elements ------


A basic unit of JSX is called a JSX element.

Here's an example of a JSX element:

```javascript
<h1>Hello world</h1>
```

This JSX element looks exactly like HTML! The only noticeable difference is that you would find it in a JavaScript file, instead of in an HTML file.

---- JSX Elements & their surroundings ------

JSX elements are treated as JavaScript expressions. They can go anywhere that JavaScript expressions can go.

That means that a JSX element can be saved in a variable, passed to a function, stored in an object or array...you name it.

Here's an example of a JSX element being saved in a variable:

```javascript
var navBar = <nav>I am a nav bar</nav>;
```

Here's an example of several JSX elements being stored in an object:
```javascript
var Pistons2004 = {
  center:        <li>Ben Wallace</li>,
  powerForward:  <li>Rasheed Wallace</li>,
  smallForward:  <li>Tayshaun Prince</li>,
  shootingGuard: <li>Richard Hamilton</li>,
  pointGuard:    <li>Chauncey Billups</li>
};
```
---- Attributes in JSX ------

JSX elements can have attributes, just like HTML elements can.

A JSX attribute is written using HTML-like syntax: a name, followed by an equals sign, followed by a value. The value should be wrapped in quotes, like this:
```javascript
my-attribute-name="my-attribute-value"
```
Here are some JSX elements with attributes:
```javascript
<a href="http://www.yahoo.com">Welcome to the Yahoo</a>;

var title = <h1 id="title">Introduction to React.js: Part I</h1>;
```
A single JSX element can have many attributes, just like in HTML:
```javascript
var panda = <img src="images/panda.jpg" alt="panda" width="500px" height="500px" />;
```
---- Nested JSX ------

You can nest JSX elements inside of other JSX elements, just like in HTML.

Here's an example of a JSX h1 element, nested inside of a JSX <a> element:
```javascript
<a href="https://www.google.net"><h1>Click me I am Google</h1></a>
```
To make this more readable, you can use HTML-style line breaks and indentation:
```javascript
<a href="https://www.google.net">
  <h1>
    Click me I am Goooogle
  </h1>
</a>
```
If a JSX expression takes up more than one line, then you should wrap the multi-line JSX expression in parentheses. This looks strange at first, but you get used to it:
```javascript
(
  <a href="https://www.google.net">
    <h1>
      Click me I am Goooooogle
    </h1>
  </a>
)
```
Nested JSX expressions can be saved as variables, passed to functions, etc., just like non-nested JSX expressions can! Here's an example of a nested JSX expression being saved as a variable:
```javascript
 var theGoogle = (
   <a href="https://www.google.net">
     <h1>
       Click me I am Gooooooooooogle
     </h1>
   </a>
 );
```
---- JSX Outer Elements ------

There's a rule that we haven't mentioned: a JSX expression must have exactly one outermost element.

In other words, this code will work:
```javascript
var paragraphs = (
  <div id="i-am-the-outermost-element">
    <p>I am a paragraph.</p>
    <p>I, too, am a paragraph.</p>
  </div>
);
```
But this code will not work:
```javascript
var paragraphs = (
  <p>I am a paragraph.</p>
  <p>I, too, am a paragraph.</p>
);
```
The first opening tag and the final closing tag of a JSX expression must belong to the same JSX element!

It's easy to forget about this rule, and end up with errors that are tough to diagnose.

If you notice that a JSX expression has multiple outer elements, the solution is usually simple: wrap the JSX expression in a <div></div>.

---- Rendering JSX ------

The following code will render a JSX expression:
```javascript
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(<h1>Hello world</h1>, document.getElementById('app'));
```
JavaScript is case-sensitive, so make sure to capitalize ReactDOM correctly!

ReactDOM is the name of a JavaScript library. This library contains several React-specific methods, all of which deal with the DOM in some way or another.

Move slightly to the right, and you can see one of ReactDOM's methods: ReactDOM.render.

ReactDOM.render is the most common way to render JSX. It takes a JSX expression, creates a corresponding tree of DOM nodes, and adds that tree to the DOM. That is the way to make a JSX expression appear onscreen.

Move to the right a little more, and you come to this expression:
```javascript
<h1>Hello world</h1>
```
This is the first argument being passed to ReactDOM.render. ReactDOM.render's first argument should be a JSX expression, and it will be rendered to the screen.

Move to the right a little more, and you will see this expression:
```javascript
document.getElementById('app')
```
ReactDOM.render makes it's first argument appear onscreen. It is appended to whatever element is selected by the second argument.

That element acted as a container for ReactDOM.render's first argument! At the end of the previous exercise, this appeared on the screen:
```javascript
<main id="app">
  <h1>Hello world</h1>
</main>
```

---- Passing a Variable to ReactDom.render() ------

ReactDOM.render()'s first argument should evaluate to a JSX expression, it doesn't have to literally be a JSX expression.

The first argument could also be a variable, so long as that variable evaluates to a JSX expression.

In this example, we save a JSX expression as a variable named toDoList. We then pass toDoList as the first argument to ReactDOM.render:
```javascript
var toDoList = (
  <ol>
    <li>Learn React</li>
    <li>Become a Developer</li>
  </ol>
);

ReactDOM.render(
  toDoList,
  document.getElementById('app')
);
```

---- The virtual DOM ------

One special thing about ReactDOM.render is that it only updates DOM elements that have changed.

That means that if you render the exact same thing twice in a row, the second render will do nothing:

```javascript
var hello = <h1>Hello world</h1>;

// This will add "Hello world" to the screen:

ReactDOM.render(hello, document.getElementById('app'));

// This won't do anything at all:

ReactDOM.render(hello, document.getElementById('app'));
```

This is significant! Only updating the necessary DOM elements is a large part of what makes React so successful.

React accomplishes this thanks to something called the virtual DOM. Before moving on to the end of the lesson, read this article about the Virtual DOM. (https://www.codecademy.com/articles/react-virtual-dom)

The Problem

DOM manipulation is the heart of the modern, interactive web. Unfortunately, it is also a lot slower than most JavaScript operations.

This slowness is made worse by the fact that most JavaScript frameworks update the DOM much more than they have to.

As an example, let's say that you have a list that contains ten items. You check off the first item. Most JavaScript frameworks would rebuild the entire list. That's ten times more work than necessary! Only one item changed, but the remaining nine get rebuilt exactly how they were before.

Rebuilding a list is no big deal to a web browser, but modern websites can use huge amounts of DOM manipulation. Inefficient updating has become a serious problem.

To address this problem, the people at React popularized something called the virtual DOM.

The Virtual DOM

In React, for every DOM object, there is a corresponding "virtual DOM object." A virtual DOM object is a representation of a DOM object, like a lightweight copy.

A virtual DOM object has the same properties as a real DOM object, but it lacks the real thing's power to directly change what's on the screen.

Manipulating the DOM is slow. Manipulating the virtual DOM is much faster, because nothing gets drawn onscreen. Think of manipulating the virtual DOM as editing a blueprint, as opposed to moving rooms in an actual house.

How it helps

When you render a JSX element, every single virtual DOM object gets updated.

This sounds incredibly inefficient, but the cost is insignificant because the virtual DOM can update so quickly.

Once the virtual DOM has updated, then React compares the virtual DOM with a virtual DOM snapshot that was taken right before the update.

By comparing the new virtual DOM with a pre-update version, React figures out exactly which virtual DOM objects have changed. This process is called "diffing."

Once React knows which virtual DOM objects have changed, then React updates those objects, and only those objects, on the real DOM. In our example from earlier, React would be smart enough to rebuild your one checked-off list-item, and leave the rest of your list alone.

This makes a big difference! React can update only the necessary parts of the DOM. React's reputation for performance comes largely from this innovation.

In summary, here's what happens when you try to update the DOM in React:

The entire virtual DOM gets updated.
The virtual DOM gets compared to what it looked like before you updated it. React figures out which objects have changed.
The changed objects, and the changed objects only, get updated on the real DOM.
Changes on the real DOM cause the screen to change.
