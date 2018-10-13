+++
date = "2018-03-31"
title = "A Beginner's Introduction to Variables"

+++
In the spirit 👻of keeping things simple and at a beginner level I am going to attempt to explain one of the fundamental aspects of javascript and programming in general, **variables**. Variables was one of the first concepts that I encountered when I started to learn to code and is one of the easiest to grasp. 

## What are Variables?

**Variables are simply containers for storing things called values**. If you're like me you've only ever encountered variables in Mathematics😱 and they are fundamentally the same in programming.

**Both x and y are variables and store the values 10 and 20 + 2 respectively**
x = 10
y = 20 + 2

You can think of x and y as boxes with names x and y that store the number 10 and formula 20 + 2 respectively. This is useful because we can then refer to those variables by their names and use them elsewhere.

x + y is the same thing as 10 + 20 +2

*Note that the above examples work fine in mathematics, however, as we will see, variables are assigned values in a specific way in javascript.*

## How are Variables Created in Javascript?

Knowing what variables are is all good and well, but how do I create and use them in javascript. Creating a variable is known as **declaring** it in javascript. The first time you declare or better yet **initialise** a variable you use the following format:

```js
var someVariable = 25;
```

**var** is a keyword which means..you guessed it variable, someVariable is the variable name or **identifier** and **25** is the number stored within someVariable. The = is the **assignment operator** and everything on the right of the assignment operator is evaluated first before that value is assigned to the variable on the left of the assignment operator.

```js
var someEquation = 22;
someEquation = someEquation + 2; 
someEquation = 24; // 22 (the previous value of someEquation) is added to 2 before
// someEquation is given its new value 24. 
```

The semi-colon is analogous to a full-stop and lets the program know that you're finished declaring the variable. 

Note that the variable name can be anything you want provided that it follows these rules: 

-   Names can contain letters, digits, underscores, and dollar signs.
-   Names must begin with a letter
-   Names can also begin with $ and _ (but we will not use it in this tutorial)
-   **Names are case sensitive (y and Y are different variables)** - pay attention to this one as it will save you from lots of frustration. 
-   Reserved words (like JavaScript keywords) cannot be used as names

## How to Use Variables?

Alright, so now that we know what variables are and how to declare them now you'll get a taste of how variables can be used. 

![#saltbae](https://media.giphy.com/media/l4Jz3a8jO92crUlWM/giphy.gif)

```js
var quick = 2 + 2;
var maths = 1;
quick - maths; // 4-1 evaluates to 3
quick = 10; // This changes the value of the variable quick to 10.
quick - maths; // This now evaluates to 9
var fyah = "man's";
var inTheBooth = " not hot";
console.log(fyah + inTheBooth); // This logs "man's not hot" to the console. 
```

As you can see variables can be easily changed from one value to another 🔥🔥. Note that you only use the keyword  `var`  when you're  _creating_  a new variable, not when you're  _editing_  one. 

Hopefully you've been able to learn a thing or two from this short introduction to variables. Feel free to give your feedback and suggestions and ask any questions that you may have, I'll try my best to answer them. 😬

## References
https://www.w3schools.com/js/js_variables.asp
http://jsforcats.com/