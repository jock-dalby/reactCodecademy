---- IF statements that DON'T work ------

Here's a rule that you need to know: you can not inject an if statement into a JSX expression.

This code will break:
```javascript
(
  <h1>
    { if (purchase.complete) 'Thank you for placing an order!' }
  </h1>
)
```
The reason why has to do with the way that JSX is compiled.

---- IF statements that DO work ------


How can you write a conditional, if you can't inject an if statement into JSX?

Well, one option is to write an if statement, and not inject it into JSX.

```javascript
var React = require('react');
var ReactDOM = require('react-dom');

if (user.age >= drinkingAge) {
  var message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  var message = (
    <h1>
      Hey, check out these earrings I got at Claires!
    </h1>
  );
}

ReactDOM.render(
  message,
  document.getElementById('app')
);
```
This works, because the words if and else are not injected in between JSX tags. The if statement is on the outside, and no JavaScript injection is necessary.

---- The Ternary operator ------

This is a common way to express conditionals in JSX.

There's a more compact way to write conditionals in JSX: the ternary operator.

The ternary operator works the same way in React as it does in regular JavaScript. However, it shows up in React surprisingly often.

Recall how it works: you write x ? y : z, where x, y, and z are all JavaScript expressions. When your code is executed, x is evaluated as either true or false. If x evaluates to true, then the entire ternary operator returns y. If x evaluates to false, then the entire ternary operator returns z.

Here's how you might use the ternary operator in a JSX expression:
```javascript
var headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);
```
---- The && operator ------

Like the ternary operator, && is not React-specific, but it shows up in React surprisingly often.

In the last two lessons, you wrote statements that would sometimes render a kitty and other times render a doggy. && would not have been the best choice for those lessons.

&& works best in conditionals that will sometimes do an action, but other times do nothing at all.

Here's an example:
```javascript
var tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```
Every time that you see && in this example, either some code will run, or else no code will run.

---- map in JSX ------

The array method .map comes up often in React. It's good to get in the habit of using it alongside JSX.

If you want to create a list of JSX elements, then .map is often your best bet. It can look odd at first:
```javascript
var strings = ['Home', 'Shop', 'About Me'];

var listItems = strings.map(function(string){
  return <li>{string}</li>;
});

<ul>{listItems}</ul>
```
In the above example, we start out with an array of strings. We call .map on this array of strings, and the .map call returns a new array of <li>s.

On the last line of the example, note that {listItems} will evaluate to an array, because it's the returned value of .map! JSX <li>s don't have to be in an array like this, but they can be.

```javascript
// This is fine in JSX, not in an explicit array:

<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>

// This is also fine!

var liArray = [
  <li>item 1</li>,
  <li>item 2<li>,
  <li>item 3</li>
];

<ul>{liArray}</ul>
```

---- Keys in JSX ------

When you make a list in JSX, sometimes your list will need to include something called keys:
```javascript
<ul>
  <li key="li-01">Example1</li>
  <li key="li-02">Example2</li>
  <li key="li-03">Example3</li>
</ul>
```
A key is a JSX attribute. The attribute's name is key. The attribute's value should be something unique, similar to an id attribute.

keys don't do anything that you can see! React uses them internally to keep track of lists. If you don't use keys when you're supposed to, React might accidentally scramble your list-items into the wrong order.

Not all lists need to have keys. A list needs keys if either of the following are true:

The list-items have memory from one render to the next. For instance, when a to-do list renders, each item must "remember" whether it was checked off. The items shouldn't get amnesia when they render.
A list's order might be shuffled. For instance, a list of search results might be shuffled from one render to the next.
If neither of these conditions are true, then you don't have to worry about keys. If you aren't sure then it never hurts to use them!

---- React.createElement ------

You can write React code without using JSX at all!

The majority of React programmers do use JSX, and we will use it for the remainder of this tutorial, but you should understand that it is possible to write React code without it.

The following JSX expression:
```javascript
var h1 = <h1>Hello world</h1>;
```
can be rewritten without JSX, like this:
```javascript
var h1 = React.createElement(
  "h1",
  null,
  "Hello, world"
);
```
When a JSX element is compiled, the compiler transforms the JSX element into the method that you see above: React.createElement(). Every JSX element is secretly a call to React.createElement().

We won't go in-depth into how React.createElement() works, but you can start with the documentation https://facebook.github.io/react/docs/top-level-api.html#react.createelement

```javascript
var greatestDivEver = React.createElement(
"div",
null,
"i am div"
);
```
