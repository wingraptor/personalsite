+++
date = "2018-10-13"
title = "The Keyword this"

+++
## What is the keyword this?

'this' is a reserved word in Javascript and is usually determined by how a function is called, i.e., its **execution context**.  Its value is determined at execution. The value of the keyword this can determined using four "rules":

1. Global Rule
2. Object/implicit Rule
3. Explicit Rule
4. Keyword new Rule

### 1. Global Context
Occurs when the keyword 'this' is outside of a **declared object**. The value of the keyword 'this' therefore refers to the global object which is the window object for Javascript run in the browser. 

```javascript
// In this case 'this' refers to the window object.
console.log(this); // window
```
&nbsp;

When variables are declared in the global scope, it is actually an object of the window (in the browser). It is attached to the window object.

```javascript
//BELOW PERSON IS DECLARED IN GLOBAL SCOPE
var person = "Mary";
// person is actually attached to the window object and hence, see below:
window.person === "Mary"
```
&nbsp;
 
Even if the keyword this occurs in a function, but is still not declared in an object, it still value still refers to the global scope:

```javascript
function whatIsThis(){
	return this;   // Returns window because this was never declared in an object.
}
whatIsThis() // window

function variableInThis(){
	//since the value of this is the window
	// all we are doing here is creating a global variable
	this.person = "Mary"; // This is bad practice, good practice is to declare global variables at the top of our code, and assign values later
}
console.log(person)// Mary
```
&nbsp;

#### Global Context and Strict Mode

Strict mode assigns the value of this inside of a function but not declared in an object to undefined. Strict mode can be enabled by including `"use strict"` in our code. This prevents us from accidentally declaring global variables by referring to an undeclared 'this' in a function which, without strict mode, will assign that variable a value in the global scope

```javascript
"use strict"
console.log(this); // window
function whatIsThis(){
	return this;  
}
whatIsThis() // undefined

function variableInThis(){
	//since we are in strict mode this is undefined
	// so what happens if we add a property on undefined
	this.person = "Mary";
}
variableInThis() //TypeError, can't set person on undefined.
// This happens because in strict mode, 'this' is undefined when the keyword this is not declared in an object and is in a function.
```
&nbsp;

---

### 2.  Implicit /Object Rule
When the keyword 'this' is inside of a declared object, the value of the keyword this will always be the closest parent object.

```javascript
var person = {
	firstName: "Ellie",
	sayHi: function(){
		return "Hi" + this.firstname;
	},
	determineContext: function(){
		return this === person;
	}
}
person.sayHi() // "Hi Ellie"
determineContext() // true
```

&nbsp;

#### Nested Object

```javascript
var person = {
	dog: {
		sayHi: function(){
			return "Hello" + this.firstname;
		},
		determineContext: function(){
			return this === person;
		},
	}
}
person.dog.sayHi(); // Hello undefined
person.dog.determineContext(); // false
```
&nbsp;

---

### 3. Explicit Rule
We can explicitly state what the value of the keyword 'this' will be by using call, apply or bind methods. 

**These three methods can only be used by functions and no other datatype.** 

Name of Method | Parameters | Invoke Immediately?
-------- | -----| ----
Call | thisArg,a,b,c,d... | YES
Apply |thisArg,[a,b,c,d...]|YES
Bind | thisArg,a,b,c,d... |NO

**thisArg** refers to the value that we want the keyword 'this' to be; we explicitly state what the value of the keyword 'this' should be in the method. a,b,c,d refer to the arguments that we are passing to the method for which we have explictly givent the keyword 'this' the value of thisArg.
&nbsp;


**Using The Call Method**

In the example below, we explicitly change the value of 'this' in the sayHello function by calling the **call** method and passing 'person' as an argument. Person refers to the person object and thus this is explicitly given the value person.

```javascript
var person = {
	firstName: "Ellie",
	sayHi: function(){
		return "Hi" + this.firstname;
	},
	determineContext: function(){
		return this === person;
	}
	dog: {
		sayHello: function(){
			return "Hello" + this.firstname;
		},
		determineContext: function(){
			return this === person;
		},
	}
}
person.dog.sayHello.call(person); // Hello Ellie
person.dog.determineContext.call(person); // true
```
&nbsp;

**Example: Using Call To DRY up Our Code**

The code below works, however, we have duplicated our code. We can however, tidy this up using the call method.
```javascript
var colt = {
  firstName: "Colt",
  sayHi: function(){
    return "Hi" + this.firstName;
  }
}

var elie = {
  firstName: "Ellie",
  sayHi: function(){
    return "Hi" + this.firstName;
  }
}

colt.sayHi(); // Hi Colt
ellie.sayHi(); // Hi Ellie
```
&nbsp;

**Refactored Code**							
```js
var colt = {
  firstName: "Colt",
  sayHi: function(){
    return "Hi" + this.firstName;
  }
}
var ellie = {
	firstName: "Ellie:
}

colt.sayHi(); //Hi Colt
colt.sayHi.call(ellie); // Hi Ellie
```
&nbsp;

**Using The Apply Method**

In the example below we can see that call and apply work in the same way, but apply takes the arguments as an apply of values.

```javascript
var colt = {
	firstName: "Colt",
	sayHi: function(){
		return "Hi" + this.firstName
	}, 
	addNumbers: function(a,b,c,d){
		return this.firstName + "just calculated" + (a+b+c+d);
	}
}

var ellie = {
	firstName: "Ellie"
}
colt.addNumbers(1,2,3,4); // Colt just calculated 10
colt.addNumbers.call(ellie,1,2,3,4);  //Ellie just calculated 10
colt.addNumbers.apply(ellie, [1,2,3,4]) //Ellie just calculated 10
```
&nbsp;

**Using The Bind Method**

The bind method works just like the call method, but instead of calling the method right away, it returns a function definition with the keyword this set to the value of the first argument in the bind method. 

1. Bind is useful when we do not know all of the arguments that will be passed to the function; we do not want to invoke the function right away but want to return a new function with some parameters set. This is known as **partial application**.

```javascript
var colt = {
	firstName: "Colt",
	sayHi: function(){
		return "Hi" + this.firstName
	},
	addNumbers: function(a,b,c,d){
		return this.firstName + " just calculated " + (a+b+c+d);
	}
}
var ellie = {
	firstName: "Ellie"
}

var ellieCalc = colt.addNumbers.bind(ellie, 1,2,3,4)
ellieCalc(); // Ellie just calculated 10.

//Alternatively, we can pass some of the arguments, 
//create the function definition and then call the function by passing more parameters.

var ellieCalc2 = colt.addNumbers.bind(ellie, 1,2); // 
ellieCalc2(3,4,); // Ellie just calculated 10.
//(1+2) were passed in as function was defined, 
//(3+4) were passed in on function call.
```

&nbsp;

2. Bind is also useful for asynchronous programming. The setTimeout method takes two arguments, the function that will be called and the time interval in ms-1. It is actually a method of the window object. 

In the code below, 'this' actually refers to the window; because setTimeout is a method of the window and therefore the function is executed in the global context . 
```js
var colt = {
	firstName: "Colt",
	sayHi: function(){
		setTimeout(function(){
			console.log("Hi" + this.firstName)
		}, 1000)
	}
}

colt.sayHi(); // Hi undefined ...after 1 second
// (this.firstName == undefined because there is no firstName key in the window object)
```
We can use bind in order to solve this problem, such that 'this' takes on the value of 'colt'. In this case, the 'this' argument of the bind method actually refers to the closest parent object, which is in this case 'colt'. Bind method then binds the value of 'colt' to the 'this' inside of the setTimeout function. Bind allows us to give the correct context to the 'this' keyword in the setTimeout function and allows it to be called after 1 second. If we were to use call or apply the function would execute immediately

```js
var colt = {
	firstName: "Colt",
	sayHi: function(){
		setTimeout(function(){
			console.log("Hi" + this.firstName)
		}.bind(this), 1000);
	}
}
colt.sayHi(); // Hi Colt...after 1 second
```
&nbsp;

---

### 4. The 'new' keyword
The new keyword allows to create a new object. We can set the context of the 'this' keyword by using the 'new' keyword.

'new' does several things: 

- Creates an empty object
- Sets the keyword 'this' to be that of an empty object
- Adds the line 'return this' to the end of the function.
- Adds a property onto the empty object called "\_\_proto\_\_" (called dunder proto), which links the prototype property on the constructor function to the empty object.

In the Person function, be default, 'this' would refer to the global context and have a value of window, however, because we use the new keyword, we can set the context to the ellie variable and 'this' takes on a value of ellie. 

```javascript
function Person(firstname,lastname){
	this.firstName = firstname
	this.lastName = lastname
}

var ellie = new Person("ellie", "Goulding");
ellie.firstName //"Ellie"
ellie.lastName // "Goulding"
```