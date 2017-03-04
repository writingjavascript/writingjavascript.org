---
layout: post
title: "Creating functions for tagged template literals"
published: true
contributors: [sethvincent]
topics: [tagged-template-literals, template-literals]
description: "Learn to write tag functions for tagged template literals"
updated: "February 3, 2017"
---

## What are tagged template literals?

Tagged template literals are functions that take strings and expressions as parameters and return a value based on those parameters.

It's an API that makes simple many tasks related to creating and parsing strings.

Tagged template literals are an extension to _template literals_. Both are new additions to JavaScript as part of ES2015.

### What are template literals?

OK, _tagged template literals_ are based on _template literals_, but what are those?

Template literals are multiline strings that use backticks instead of quotes, and that allow interpolation of values and expressions using a dollar symbol and curly brackets: `${}`.

Here's an example of a template literal:

```js
var x = 3
var example = `${x} is a number`
console.log(example)
```

This logs: `3 is a number`.

### Tag a template literal with a function

So if a template literal is a multiline string with interpolation, a tagged template literal is a way to process that string and the values passed in through interpolation.

## Using tagged template literals

An example of a tagged template literal is the [bel](https://npmjs.com/bel) module.

It's useful for creating composable DOM elements.

Here's an example:

```js
var bel = require('bel')

var div = bel`<div>hello</div>`
```

The `div` variable is an object that can be added directly to the DOM:

```js
var bel = require('bel')

var div = bel`<div>hello</div>`

// add the div to the dom
document.body.appendChild(div)
```

## Creating tagged template literals

A tag function is a function that's used to tag template literals that parses and modifies strings to produce some value.

The first parameter to a tag function is an array of strings.

Any following parameters are the values passed into the template literal using interpolation.

### Minimal example of a tag function

Let's start with a minimal example that replicates the behavior of a template literal.

```js
function createString () {
  var strings = arguments[0]
  var values = Array.prototype.slice.call(arguments, 1)

  return strings.reduce(function (result, string, i) {
    return result + string + (values[i] ? values[i] : '')
  }, '')
}
```

The above function shows:

- the first argument is an array of strings
- that array is the original template string, split wherever an interpolated expression occurs
- all the following arguments are the values that are passed in via interpolation
- the function returns the concatenated strings and values

Example usage:

```js
var example = createString`hey ${'hi'}`
console.log(example)
```

This logs: `hey hi`

### Coverter a string of key: value statements to an object

Let's make a tag function that coverts a multiline string like this:

```
a: 1
b: 2
c: 3
```

Into an object like this:

```js
{
  a: 1,
  b: 2,
  c: 3
}
```

To get started, we'll start with a function named `keyValue` that looks similar to our last tag function:

```js
function keyValue () {
  var strings = arguments[0]
  var values = Array.prototype.slice.call(arguments, 1)
}
```

We're going to return an object from this function, so let's get that set up:

```js
function keyValue () {
  var strings = arguments[0]
  var values = Array.prototype.slice.call(arguments, 1)
  var obj = {}

  return obj
}
```

Now, we need to parse the strings and values and assign properties to that object:

```js
function keyValue () {
  var strings = arguments[0]
  var values = Array.prototype.slice.call(arguments, 1)
  var obj = {}

  strings.forEach(function (string, i) {
    if (values[i]) {
      string = string + values[i]
    }

    var lines = string.split('\n')

    lines.forEach(function (line) {
      if (line.length) {
        var kv = line.trim().split(':')
        var key = kv[0].trim()
        var value = kv[1].trim()
        var num = parseFloat(value)
        obj[key] = num ? num : value
      }
    })
  })

  return obj
}
```

Note that this example also checks values to see if they are numbers, and parses them appropriately.


Example usage of the `keyValue` tag function:

```js
var example = 'hi'

var result = keyValue`
a: b
message: ${example}
c: 1
`

console.log(result)
```

This logs:

```js
{
  a: 'b',
  message: 'hi',
  c: 1
}
```

I've turned this example into a simple module called [kv-tag](http://github.com/sethvincent/kv-tag).

### Using rest parameters

Since you're probably using an environment or build tool that allows ES2015+ code, here's a refactored version of the `keyValue` tag function that takes advantage of rest parameters to make things simpler:

```js
function kvTag (strings, ...values) {
  var obj = {}

  strings.forEach(function (string, i) {
    if (values[i]) {
      string = string + values[i]
    }

    var lines = string.split('\n')

    lines.forEach(function (line) {
      if (line.length) {
        var kv = line.trim().split(':')
        var key = kv[0].trim()
        var value = kv[1].trim()
        var num = parseFloat(value)
        obj[key] = num ? num : value
      }
    })
  })

  return obj
}
```

The above example isn't much different! But the `...values` rest parameter allows us to remove a couple lines to make the function simpler.

## Examples of modules using tagged template literals

- [emojify-tag](https://npmjs.com/emojify-tag) – turns emoji codes into unicode
- [yo-yo](https://npmjs.com/yo-yo) – create & update DOM elements (uses bel)
- [bel](https://npmjs.com/bel) – create DOM elements (uses hyperx)
- [hyperx](https://npmjs.com/hyperx) – tagged template string virtual dom builder compatible with bel, virtual-dom, react, etc.
- [beldown](https://npmjs.com/beldown) & [belmark](https://npmjs.com/belmark) – tag functions that turn markdown into DOM elements with bel
- [backtick](https://npmjs.com/backtick) – template literal based template engine
- [sheetify](https://npmjs.com/sheetify) – modular CSS bundler
- [styled-components](https://npmjs.com/styled-components) – create styled react components with tagged template strings
