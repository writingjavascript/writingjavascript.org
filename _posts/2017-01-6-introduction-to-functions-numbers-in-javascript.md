---
layout: post
title: "Introduction to functions & numbers in JavaScript"
published: true
contributors: [sethvincent]
topics: [strings, template-literals, functional-programming]
description: "Write a function that adds numbers"
updated: "January 6, 2017"
---

## The goals for this post

- Get familiar with JavaScript syntax and data types.
- Write a function that does one task really well.
- Try out the Chrome JavaScript console
- Learn about debugging and refactoring code.

This post is meant for beginners that would like a friendly introduction to writing functions in JavaScript. Let's get started:

## Write JavaScript on paper

- Take out a sheet of paper and a pen.
- Write the following on the paper:

```js
var x = 1
var y = 2
var z = x + y
```

This is JavaScript! What are we doing here?

You know what happens when you write `x + y`. We're adding those two numbers together.

You already know the value of `z`.

This looks just like math, and that's because it is.

Writing code isn't all about math, but working with numbers is a significant part of the work you'll be doing on a daily basis.

**If the above is simple math, what's with the word `var`? What's that?**

The word `var` stands for variable. We use it only when creating a variable. You might remember the concept of variables from math, too. In this case, `x` is just a name that refers to the number 1. Any time we want to create a variable in JavaScript, we write something like:

```js
var nameOfTheVariable = 'whatever the variable should reference'
```

**Why are there single quotes around the phrase `whatever the variable should reference`?**

Check out the `var x = 1` statement above. There aren't any quotes around the `1`. This is how we can tell numbers from text. In JavaScript (and most programming languages), text like this is called a **string**.

**Wait, why did I just write that on paper?**

Asking you to write code on paper wasn't arbitrary. It's useful to think about code in different ways, especially in the abstract. Sometimes it takes brainstorming away from the computer to figure out solutions to difficult problems. Another perk to paper coding: your program doesn't have to run, so you can use _pseudocode_.

**So, what's pseudocode?**

Here's a simple example:

```
if x is greater than 10, subtract 1 from x.
```

Here's that pseudocode turned into JavaScript:

```js
if (x > 10) {
  x = x - 1
}  
```

We won't go into `if` statements in detail here, but based on this pseudocode you should be able to tell what's happening in that JavaScript.

## Pseudocode is awesome

You can use pseudocode to experiment, and to define the outline of a program without worrying about errors or syntax details. It's a great way to start thinking about the structure of the code you're about to write.

**Now let's open up the web browser, Chrome, and do some experimenting.**

> If you haven't installed Chrome yet, do so now at [google.com/chrome](http://google.com/chrome)

1.  Open a Chrome window.
2.  Go to a website, like [superbigtree.com](http://superbigtree.com).
3.  On a mac, click **View**, in the top menu, hover over **Developer**, then click **JavaScript Console**.> You can also use a keyboard shortcut: Command+Option+J on macOS.

If you've used a terminal program on your computer, the JavaScript console is similar, except you write JavaScript instead of terminal commands.

**Important:**

Any time there are code samples just type them straight into the JavaScript console, hit **Enter**, and see what happens. The best way to learn a programming language is to type it a lot. More than a lot.

In the console, type:

```js
var x = 10
```

Hit enter, and you'll see the word `undefined` pop up below your line of JavaScript. That's fine, it's normal. That's what the console returns when you enter such a statement. To see the value of `x`, type `x` into the console.

The console should return the number `10`!

## Let's get functional

Consider this pseudocode:

```js
add two arbitrary numbers
```

We're going to create a function in JavaScript that adds two numbers.

We'll create a function named `add`, and it takes two arguments and adds them together. For now, we assume the arguments to be numbers.

Before implementing the `add` function,  before writing the code that makes it work, it's useful to sketch out what _usage_ of the function might look like.

To use the `add` function, we'll write something like this:

```js
add(3, 7)
```

That looks good! That gives us some good clues about what we'll want to keep in mind when implementing the function.

### Let's add with a function

A function is a block of executable code, and when we give a function a name, like we do below, it can be used throughout your program. The benefit: define a function once rather than using similar blocks of code in multiple places in your program.

```js
function add (x, y) {
  return x + y
}
```

Type the above `add` function into the JavaScript console, and use it to do some addition!

> **Important note:** using Chrome's JavaScript console, if you hit **Enter** it will execute the code. To type a function like this onto multiple lines, hit **Shift + Enter** to add a line.

Just like with the variables we created earlier, when we first define a function in the console it will return `undefined` when you hit enter. This is normal.

> **Tip:** When you are in the JavaScript console you can hit the up arrow to revisit previous code that you've typed in.

### Try these examples

```js
// add 2 and 4
add(2, 4)

// create a variable named num and set its value to the sum of 3 and 4
var num = add(3, 4)
```

### Hey, you made `num` equal the usage of the add function

That's right!. Let's take a look at the definition of the `add` function again:

```js
function add (x, y) {
  return x + y
}
```

Check out the middle line, `return x + y`.

With most JavaScript programming, one of your goals should be to write small, simple functions that take arguments as input, modify that input, and output it using the `return` statement. The value that a function returns is used elsewhere in your program.

When we make the variable `num` equal `add(3, 4)`, we're really setting `num` reference the value that's returned from the add function. In this case, `add(3, 4)` will return the number 7, so that's what `num` references.

### Wait, what if I messed up the adder?

Hey, sorry to bother you, but somebody tried to use our add function like this:

```js
add('1', '5')
```

Unsurprisingly, it didn't work as expected. Can you guess what the `add` function returned?

It returned this: `'15'`.

That's embarrassing. `'15'` isn't even a number in JavaScript! It's a string. We can tell by those quotes surrounding the text.

### Why didn't it add?

Those numbers had quotes around them. Numbers in JavaScript do not have quotes around them, only strings. Instead of adding numbers, our program combined two strings.

### Walking like a duck

JavaScript is a dynamically-typed language. Remember how we created variables earlier that referenced specific values? Each value that a variable references has a type, and in JavaScript, you don't have to specify a type when you create a variable. You can change a variable's type later in the program, and you will interact with a variable in different ways depending on its type.

#### Here are common types:

**Boolean:** `true` or `false`

**Example:**

```js
var thisIsFalse = false
var thisIsTrue = true
```

Note that there are no quotes around the words `true` or `false`. The variable named `thisIsTrue` references the value `true`, and the variable named `thisIsFalse` references the value `false`.

**Number:** integer or float

**Example:**

```js
var thisIsAnInteger = 123
var thisIsAFloat = 3.14
```

A float is a number with a decimal. An integer is a whole number, without a decimal.

**String:** text in quotes.

**Example:**

```js
var thisIsAString = 'you can tell because this text is inside of quotes'
```

A string is any text inside of quotes. It can be single or double quotes, but it has to be the same on each end. This will work: `'text'`, and this will work: `"text"`, but this will not work: `'text"`.

In newer versions of JavaScript, strings can also be inside backticks, like this:

```
`This is a string
on multiple
lines`
```

Strings inside backticks allow you to have multiple lines and are called [template literals](/template-literals).

### Back to our addition issue:

This usage of our function doesn't work: `add('1', '5')`.

The reason? The `+` operator and the way it works with strings.

This little buddy does a little more than you might expect at first. It'll add numbers together, but it'll also add strings together. When that happens it's called concatenation.

When we use the `add` function with `'1'` and `'5'` as arguments, it executes a statement like this:

```js
return '1' + '5'
```

A string `+` a string equals those two strings combined. That's concatenation. So `'1' + '5'` becomes `'15'`.

**Some examples:**

```js
'abc' + 'def' // becomes 'abcdef'
'This is a ' + 'string' // becomes 'This is a string'`
'1' + '5' // becomes '15'`
```

Lets add some code to our `add` function to make sure this doesn't happen. By converting the arguments of the function to numbers, we can allow for the possibility of adding numbers that happen to be strings!

```js
function add (x, y) {
  return parseInt(x) + parseInt(y)
}
```

All we added was the usage of the `parseInt` function. This is a part of core JavaScript, and is used to convert strings and floats to integers.

### Now we have a `float` issue

Somebody tried to add some floats together, like this:

```js
add(3.14, 7.28)
```

It did not work as expected. It returned `10`. That's because `parseInt` is only going to return the integer it finds in a string. So maybe `parseInt` isn't the best solution.

**There is an easy fix.** Revise your add function to look like this:

```js
function add (x, y) {
  return parseFloat(x) + parseFloat(y)
}
```

Yep, that works. Now that we're using `parseFloat` instead of `parseInt`, decimal numbers stay intact. Now `add(3.14, 6.28);` returns `9.42`.

### What about adding more than two numbers?

Somebody found a weird workaround for adding multiple numbers using this `add` function:

```js
var a = add(1, 3)
var b = add(a, 7)
var c = add(b, 21)
```

Cool trick! But they should't have to do such extra work. We can make this easier. Rewrite the add function to look like this:

```js
function add () {
  var total = 0

  for (var i = 0; i < arguments.length; i++) {
    total += parseFloat(arguments[i])
  }

  return total
}
```

Now we can add any number of arguments to the `add` function and get the correct result! With this change we can now pass any number of arguments to `add`, like this:

```js
add(1, 2, 3, 4, 5, 6, 7)
```

This makes `add` much more flexible than the previous workaround.

We used a `for` loop to cycle through all the arguments that are passed to `add`. We also used a variable named `total` to reference the sum of all arguments.

### The loop: cycling through a function's arguments

Notice above we used a `for` loop. We just snuck that in there.

First we set a start value: `var i = 0`. That sets `i` to `0`, which makes our loop start at `0`.

Then compare that to an end value: `i < arguments.length`. The statement `arguments.length` gives us the number of arguments. `length` returns the number of arguments. So, with usage like this: `add(1, 2, 3)`, `arguments.length` will return `3`.

As long as `i` is less than 3, the loop will run again.

Then we give the loop an increment value: `i++`. The `++` increases `i` by one with every loop.

### One last problem: `'one'`

That's not a number. Can you guess what happens when someone tries to do this:

```js
add('one', 'two', 3)
```

Paste in the latest version of the `add` function to the Chrome JavaScript console. Then try out the above usage of `add`.

It should return something like this:

<pre>`1 NaN`
</pre>

Let's fix that. The problem: `NaN` means **not a number**. When we run `parseFloat` on a string like `'one'`, it returns `NaN`, and when we try to add `NaN` to a number, the whole sum becomes `NaN`.

There are a few possible solutions to this problem. Here are two:

**Ignore any argument that is not a number.**

```js
function add () {
  var total = 0;
  for (var i = 0; i < arguments.length; i++) {
    var num = parseFloat(arguments[i])

    if (isNaN(num) === false ) {
      total += num
    }
  }
  return total
}
```

The new code that we added is this `if` statement:

```js
var num = parseFloat(arguments[i])

if (isNaN(num) === false ) {
  total += num
}
```


The function `isNaN` checks to see if `num` is a number. If `isNaN` returns false, then we know that the argument is a number. This checks to see if an argument is a number, and if not, ignores it – but there's still a problem with this. 

Ignoring values like `'one'` in our `add` function because it doesn't contain numbers is reasonable. 

**A potential problem:** this error fails silently. Any time there's a chance a function can fail because of misuse by yourself or another programmer, it's often best for the code to send errors explaining why it fails.

Whether or not your function should silently ignore invalid arguments or throw an error is completely determined by the situations the code is likely to be used. If ignoring invalid values is documented and expected, and won't harm other parts of the program, that's ok. 

Throwing errors based on invalid arguments is only really useful for checking programming error, so we can see when we start or test a program if we've got things correct. It's not a good idea to throw errors when a function is evaluating user input or other values that are not determined by the programming. That will just make your program crash.

In this code let's switch up our code so that if an argument is not a number, `add` throws an error, and if the argument _is_ a number, it gets added to the `total` variable.

```js
function add() {
  var total = 0;

  for (var i = 0; i < arguments.length; i++){
    var num = parseFloat(arguments[i])

    if (isNaN(num)) {
      throw new Error('Arguments to `add`  must be numbers.')
    } else {
      total += num
    }
  }

  return total
}
```

Now, when we put that version of `add` into our JavaScript console and use it like this:

```js
add('one', 2)
```

It'll return an error with this text: 

```
Error: Arguments to `add` must be numbers.
```

Good, that was our goal. Now any strings that can't be converted to numbers will result in this clear error rather than being ignored.

## So here's what we covered:

- **Chrome JavaScript console:** We started using Chrome's JavaScript console.
- **Basic data types:** We covered the basics of strings, numbers, and booleans.
- **Writing functions:** We went over the basics of writing a simple function.
- **Refactoring code:** As we wrote and experimented use cases of the `add` function we identified ways it could be improved and rewrote the function to guard against mistakes.
- **Debugging and useful errors:** As you're getting started it probably feels like errors are just something to avoid. But, if we can embed useful errors in our code in places where we know there are likely problems, that can make debugging much easier.
