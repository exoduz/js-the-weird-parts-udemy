# Javascript: The Weird Parts #
#### https://www.udemy.com/understand-javascript ####


### Lecture 7 ###
*Name/Value Pair:* name which maps to a unique value
e.g. `var address = “100 Main St”;`

*Object:* collection of name/value pairs

```javascript
Address: {
	Street: Main,
	Apartment: {
		Floor: 3...
	}
}
```


### Lecture 9 ###
Execution context creates “Global Object (`window`)” and `this`
`this` refers to the ‘window' object at the global level
Global object means “not inside a function”


### Lecture 10 ###
Function can be called at anytime, even if it’s being instantiated below the call

*Hoisting:* setup memory space for variables and functions. functions and variables exist in memory
This means that no matter where the function or variable is instantiated, JS can still read it. If a variable is instantiated below the the code the it would just give an ‘undefined’.

```javascript
b(); //Called b
console.log(a); //undefined

var a = “Hello World”;

function b() {
	console.log(‘Called b’);
}
```

All variables are set to ‘undefined’

```javascript
//Always to code in logical order
var a = “Hello World”;

function b() {
console.log(‘Called b’);
}

b(); //Called b
console.log(a); //Hello World
```


### Lecture 11 ###

