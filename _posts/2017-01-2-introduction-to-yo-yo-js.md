---
layout: post
title: "Introduction to yo&#8209;yo.js"
published: true
contributors: [sethvincent]
topics: [tagged-template-literals, yo-yo, bel, morphdom]
description: "yo-yo.js is a small, friendly module for creating DOM elements as an alternative to virtual DOM modules like React."
updated: "January 3, 2017"
---

[yo-yo](https://npmjs.com/yo-yo) is a module that creates and updates DOM elements. 

Instead of using a virtual DOM like [react](https://npmjs.com/react) or [virtual-dom](https://npmjs.com/virtual-dom), yo-yo uses the actual DOM to diff 
changes and make efficient updates

yo-yo uses [tagged template strings](/tagged-template-literals) to create DOM elements.

### No JSX

Because yo-yo uses tagged template strings, we don't have to introduce a special HTML-like language. We can just write HTML inside the template strings.

### File size
 
Hoping to reduce the file size of your apps? yo-yo is 4kb minified and gzipped.

### Using yo-yo in Node.js

Want to use yo-yo on the server? You can! Elements you create have a `.toString()` method you can use to stringify the elements.

### Old browser support

You can support older browsers using the [yo-yoify browserify transform](https://npmjs.com/yo-yoify).

### Minimal dependencies

yo-yo relies on [bel](https://npmjs.com/bel) to create elements and [morphdom](https://npmjs.com/morphdom) to update elements. yo-yo also has very minimal development dependencies.

## Installing

You can install yo-yo with [npm](/npm):

```txt
npm install --save yo-yo
```

## How to use yo-yo

Here are a few yo-yo usage examples to get you started.

### Follow along:
- create a directory for this example code
- install yo-yo with npm: `npm install yo-yo`
- create a file named `index.js` to type in examples
- install budo, a development server for browserify: `npm install -g budo`

### Creating elements

To create an element, `require` the `yo-yo` module, then put html inside of the backticks after `yo`:

```js
var yo = require('yo-yo')

var element = yo`
  <p>hi</p>
`
```

### Attaching elements to the DOM

There's nothing fancy about attaching an element made with yo-yo to the DOM. Use `appendChild` to attach the element to the `body` or any other existing html:

```js
var yo = require('yo-yo')

var element = yo`
  <p>hi</p>
`

document.body.appendChild(element)
```

### Using variables

A nice part about template literals is the ability to interpolate values into the string:

```js
var yo = require('yo-yo')

var message = 'oh cool'

var element = yo`
  <p>${message}</p>
`

document.body.appendChild(element)
```

### Updating elements

To update an element we use the `yo.update` method. The first argument to `yo.update` is the existing element you want to update. The second argument is the element with the new changes that you want to add to the DOM. In this example we increase the `count` variable every second:

```js
var yo = require('yo-yo')

var count = 0

var element = yo`
  <p>count: ${count}</p>
`

setInterval(function () {
  count++
  var newElement = yo`
    <p>count: ${count}</p>
  `
  yo.update(element, newElement)
}, 1000)

document.body.appendChild(element)
```

### Updating elements in response to user input

We can use an `onclick` handler on a `<button>` element to update the count rather than updating every second:

```js
var yo = require('yo-yo')

var count = 0

var element = yo`
  <p>count: ${count}</p>
`

var input = yo`
  <button onclick=${onclick}>increase count</button>
`

function onclick () {
  count++
  var newElement = yo`
    <p>count: ${count}</p>
  `
  yo.update(element, newElement)
}

document.body.appendChild(element)
document.body.appendChild(input)
```

### Simplifying multiple elements with a render function

The above example is a little messy with the duplicate `document.body.appendChild` statements and multiple elements created with `yo`.

Let's clean up the example by using a `render` function that returns the DOM node created by `yo`. Note that when we have multiple elements we have to wrap it in a parent element so that there is only one root element:

```js
var yo = require('yo-yo')

var count = 0

function render () {
  return yo`
    <div id="app">
      <p>count: ${count}</p>
      <button onclick=${onclick}>increase count</button>
    </div>
  `
}

var app = render()

function onclick () {
  count++
  var update = render()
  yo.update(app, update)
}

document.body.appendChild(app)
```

### Supporting older browsers

It's recommended to use [browserify](https://npmjs.com/browserify) to bundle JS dependencies when using yo-yo. Additionally you can use the [yo-yoify](https://npmjs.com/yo-yoify) transform for browserify to convert tagged template literals into plain DOM-related JavaScript.

#### Example of setting up browserify & yo-yoify

Install as devDependencies:

```
npm install --save-dev browserify yo-yoify
```

Create a `bundle` npm script in your package.json file:

```
"scripts": {
  "browserify index.js -t yo-yoify -p bundle.js"
}
```

## yo-yo dependencies

### bel & morphdom

yo-yo's dependencies are [bel](https://npmjs.com/bel) and [morphdom](https://npmjs.com/morphdom). bel in turn uses [hyperx](https://npmjs.com/hyperx) to create DOM nodes from the tagged template literals, and morpddom provides the DOM diffing functionality. Try them out if you're looking for a lower-level approach to tagged template strings and DOM diffing, or want to learn more about how yo-yo works.

## Projects using yo-yo

### choo

[choo](https://npmjs.com/choo) is a pleasant little framework based on yo-yo and a handful of other small modules. Check it out if you're looking for a higher-level approach, or to get a sense of how yo-yo might fit into a larger project.
