# Javascript: The Weird Parts #
##### https://www.udemy.com/understand-javascript #####


### Lecture 7 - Conceptual Aside: Name/Value Pairs and Objects ###
*Name/Value Pair:* name which maps to a unique value, e.g. `var address = "100 Main St";`

**Object:** collection of name/value pairs

```javascript
Address: {
	Street: Main,
	Apartment: {
		Floor: 3...
	}
}
```


### Lecture 9 - The Global Environment and the Global Object ###
Execution context creates "Global Object (`window`)" and `this`  
`this` refers to the "window" object at the global level  
Global object means "not inside a function"


### Lecture 10 - The Executiion Context - Creation and Hoisting ###
Function can be called at anytime, even if it's being instantiated below the call

**Hoisting:** setup memory space for variables and functions. functions and variables exist in memory.  
This means that no matter where the function or variable is instantiated, JS can still read it. If a variable is instantiated below the the code the it would just give an 'undefined'.

```javascript
b(); //Called b
console.log(a); //undefined

var a = 'Hello World';

function b() {
	console.log('Called b');
}
```
All variables are set to `undefined`

```javascript
//Always code in logical order
var a = 'Hello World';

function b() {
console.log('Called b');
}

b(); //Called b
console.log(a); //Hello World
```


### Lecture 11 - Conceptual Aside: Javascript and 'undefined' ###
`undefined` is not just the word, it's a special value which means that the variable hasn't been set

**DO NOT** do `a = undefined`, let it mean "I, the programmer, never set it's value"


### Lecture 13 - Conceptual Aside: Single Threaded, Synchronous Execution ###
**Single Threaded:** one command at a time  
**Synchronous:** one at a time, and in order


### Lecture 14 - Function Invocation and the Execution Stack ###
**Invocation:** run/call the function  
**Execution Stack:** the order in which the functions in invoked. The more recent the function call, the higher it sits on the execution stack

![Execution Stack](img/14-01.png)

Every function creates a new execution context which runs through function line by line.

