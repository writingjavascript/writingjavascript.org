---
layout: post
title: "Introduction to browserify"
published: true
contributors: [sethvincent]
topics: [browserify]
description: "Learn to use browserify for bundling dependencies for the browser."
updated: "January 3, 2017"
---

There's all this wonderful code on [npm](https://npmjs.com). Hundreds of thousands of modules. What if we could use that code in the browser?

## Hey, we can with browserify!

With [browserify](https://github.com/substack/node-browserify), we can use the thousands of modules on `npm` in our browser-side code.

We can also write our browser-side JavaScript in the node.js style by using the `require` function.

> Browserify is one of many options for bundling JS for the browser. See the alternatives section at the end of this post for more info.

## Install browserify:

```
npm install -g browserify
```

The `-g` option installs browserify globally on your computer, allowing you to use it on the command line.

### Brief example using a core node module

Create a file named `index.js` and add this code:

```js
// require the core node events module
var EventEmitter = require('events').EventEmitter

//create a new event emitter
var emitter = new EventEmitter

// set up a listener for the event
emitter.on('pizza', function (message) {
  console.log(message)
})

// emit an event
emitter.emit('pizza', 'pizza is extremely yummy')
```

> In most cases core node modules are a little too big to regularly use in the browser. This example is just a demonstration of what's possible with the `require` statement. You may want to research lightweight alternatives to core modules when writing code for production.

Now, to be able to run this code in the browser, enter this command in the terminal:

```
browserify index.js > bundle.js
```

The bundle.js file now has your event emitter code along with any dependencies on core node modules and shims to make them work in the browser.

You can include bundle.js in your html now like any other JavaScript file.

Example:

```html
<!DOCTYPE html>
<html>
<head>
<title>browserify example</title>
</head>
<body>
<script src="/bundle.js"></script>
</body>
</html>
```

That's it! Now you can use node modules and `require` in the browser!

## Live reload development environment

If you're in the middle of writing code, you'll find running `browserify` in the terminal to regenerate bundle.js, then refreshing the browser to be time-consuming and annoying.

### Enter budo!

[`budo`](https://github.com/mattdesl/budo) is a command-line tool for automatically generating and serving your browserify bundles as you develop. It's designed to be useful for quick prototyping. Each time you save your JavaScript file `budo` will regenerate the bundle.js file and refresh the browser automatically.

Install budo:

```
npm install -g budo
```

Now, run this:

```
budo index.js:bundle.js --live
```

The `--live` option enables the live reload functionality of beefy.

The `index.js:bundle.js` is telling budo to read the contents of `index.js`, bundle the code, and serve that bundle to the browser as `bundle.js`.

This will by default serve your index.html file at [http://localhost:9966](http://localhost:9966).

Open Chrome, enter that url, then open the JavaScript console by using the keyboard shortcut `Command+Option+j`.

You'll see `pizza is extremely yummy` in the JavaScript console!


## Browserify transforms

When browserify bundles our code, we have the option to transform the code as well.

This is useful for a lot of purposes: using [babel](https://www.npmjs.com/package/babelify), [reading files on the filesystem](https://www.npmjs.com/package/brfs), [bundling css](https://www.npmjs.com/package/sheetify), and more.

### Browserify transform example using brfs

We can use transforms on the command-line using the `-t` argument:

```
browserify index.js -o bundle.js -t brfs
```

Using transforms with budo is similar. Take a look at this example:

```
budo index.js:bundle.js -- -t brfs
```

Any arguments after the `--` are passed to browserify. Arguments before the '--' are for budo.

With brfs we're able to run code like this in our index.js file:

```js
var fs = require('fs')
var path = require('path')

var content = fs.readFileSync(path.join(__dirname, 'hello.md'))
console.log(content)
```

Put some text into a file named `hello.md`, run `budo index.js:bundle.js -- -t brfs`, and you'll see the text from that file in the JavaScript console of Chrome.

When the above chunk of code is sent to the browser it ends up looking something like this:

```js
var content = 'whatever text was in that file'
console.log(content)
```

This can be useful for reading data files, templates, and whatever else exists on your filesystem that you want to share with your browser code.

Transforms can do a lot more. Check out [this list of transforms](https://github.com/substack/node-browserify/wiki/list-of-transforms).

## Using browserify programatically

Browserify isn't just a command-line tool. You can use it in node modules and applications as well.

Here's an example that does the same thing as `browserify index.js -o bundle.js`:

```js
var fs = require('fs')
var path = require('path')
var browserify = require('browserify')

var input = path.join(__dirname, 'index.js')
var output = path.join(__dirname, 'bundle.js')

var b = browserify(input)

b.bundle(function (err, buf) {
  if (err) return console.log(err)
  fs.writeFile(output, buf, function (err) {
    if (err) return console.log(err)
  })
})
```

Here's an example of using a transform programatically:

```js
var fs = require('fs')
var path = require('path')
var browserify = require('browserify')

var input = path.join(__dirname, 'index.js')
var output = path.join(__dirname, 'bundle.js')

var b = browserify(input)
b.transform('brfs')

b.bundle(function (err, buf) {
  if (err) return console.log(err)
  fs.writeFile(output, buf, function (err) {
    if (err) return console.log(err)
  })
})
```

## More browserify resources

- [github repo](https://github.com/substack/node-browserify)
- [browserify handbook](https://github.com/substack/browserify-handbook)
- [awesome browserify list](https://github.com/ungoldman/awesome-browserify)

## Alternatives to browserify

- [webpack](https://npmjs.com/webpack) – a module bundler that is heavy on configuration.
- [rollup](https://npmjs.com/rollup) – An interesting bundler focused on removing unused code and minimizing boilerplate code produced by the bundler.
