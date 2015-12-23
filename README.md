# Javascript: The Weird Parts #
##### https://www.udemy.com/understand-javascript #####


### Lecture 7 - Conceptual Aside: Name/Value Pairs and Objects ###
**Name/Value Pair:** name which maps to a unique value, e.g. `var address = "100 Main St";`

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

**Hoisting:** setup memory space for variables and functions. functions and variables exist in memory  
This means that no matter where the function or variable is instantiated, JS can still read it. If a variable is instantiated below the the code the it would just give an 'undefined'

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

![Execution Stack](http://robinjulius.com/wp-content/uploads/2015/12/14-01-1024x700.png)

Every function creates a new execution context which runs through function line by line.


### Lecture 16 - The Scope Chain ###
**Scope** Where can we find that var

```javascript
function b() {
	console.log(myVar); //1
}

function a() {
	var myVar = 2;
	b();
}

var myVar = 1;
a();
```

```javascript
function a() {
	function b() {
		console.log(myVar); //2
	}

	var myVar = 2;
	b();
}

var myVar = 1;
a();
```
Result is based on outer environment


### Lecture 20 - Conceptual Aside: Primitive Types ###
**undefined** Lack of existence (you shouldn't set a variable to this), but you can test for it  
**null** Lack of existence (you can set a variable to this)  
**boolean** true / false  
**number** _floating point_  
**string** sequence of characters ('' and "" can be used)  
**symbol** only used in ES6


### Lecture 22 - Operator Precedence and Associativity ###
[Operator Precedence and Associativity Table on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

**Associativity:** When 2 or more operators have the same precedence. Right to left or left to right, check the above link for more information


### Lecture 24 - Conceptual Aside: Coercion ###
**Coercion:** Converting a value from 1 type to another

```javascript
var a = 1 + '2'; //12
```

### Lecture 25 - Comparison Operators ###
```javascript
console.log(1 < 2 < 3); //true
console.log(3 < 2 < 1); //true, because (false < 1), will try to convert false a number which means (0 < 1) === true

Number(undefined) //NaN
Number(null) //0
```

`==` causes strange results especially with null, undefined and 0  
User `===` (strict equality) and `!==` (strict inequality)

[Equality comparisons and sameness on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Equality_comparisons_and_sameness)

### Lecture 27 - Existence and Booleans ###
```javascript
Boolean(undefined); //false
Boolean(null); //false
Boolean(''); //false
Boolean(0); //false
```


### Lecture 30 - Objects and the Dot ###
![Objects](http://robinjulius.com/wp-content/uploads/2015/12/30-01-1024x660.png)

```javascript
var person = new Object();

person["firstname"] = "John";
person["lastname"] = "Doe";

console.log(person);
console.log(person.firstname); // === person["firstname"]

person.address = new Object();
person.address.street = "111 Main St";
person.address.city = "New York";

console.log(person.address.street);
console.log(person.address.city); // === person["address"]["city"]
```


### Lecture 31 - Objects and Object Literals ###
**Object Literal:** short hand of declaring variables `var person = {};` instead of `var person = new Object();`


### Lecture 32 - Framework Aside: Faking Namespaces ###
**Namespace:** Container for variables and functions  
Use objects to fake namespaces so that it does not clash with variables of the same name

```javascript
var greet = 'Hello!';
var greet = 'Hola!';

console.log(greet); //Result: 'Hola!' because it's run synchronously one line after another

var english = {
	greet: "Hello!"
};

var spanish = {};
spanish.greet = 'Hola!';

console.log(english.greet); //Hello!
```


### Lecture 33 - JSON and Object Literals ###
`JSON.stringify()` - convert to JSON  
`JSON.parse()` - convert to JS object


### Lecture 34 - Functions are Objects ###
Function **names** are optional  
**Functions are Objects**


### Lecture 35 - Function Statements and Function Expressions ###
**Expression:** Code that results in a value

```javascript
var anonymousGreet = function () {
	console.log('hi');
}

anonymousGreet(); //invoke anonymous function

function log(a) {
	console.log(a); //will just output a string of the anonymous function below
}

function log(a) {
	a(); //hi
}

log(function () {
	console.log('hi');
});
```


### Lecture 36 - Conceptual Aside: By Value vs By Reference ###
**By value:** passing or referencing one value to another by copying the value (all primitive types)  
**By reference:** passing or referencing one value to another by pointing to address value in memory (all objects including functions)

**Mutate:** Changing something  
**Immutable:** Cannot be changed

```javascript
//by reference
var c = { greeting: 'hi' };
var d;

d = c;
c.greeting = 'hello';
f
console.log(c); //hello
console.log(d); //hello

//equals operator sets up new memory space (new address)
c = { greeting: 'howdy' };
console.log(c); //howdy
console.log(d); //hello
```


### Lecture 37 - Objects, Functions and 'this' ###
```javascript
function a() {
	console.log(this);
}

var b = function () {
	console.log(this);
}

a(); //this is global object
b(); //this is global object

var c = {
	name: 'The c object',
	log: function () {
		console.log(this);
	}
};

c.log(); //the object that the method is sitting inside of. In this case 'c'

//js bug
var c = {
	this.name: 'Updated c object';
	console.log(this); //c object - method to an object is fine

	var setname = function (newname) {
		this.name = newname; //internal functions have a problem as it points to the global object 
	}

	setname('Updated again! The c object');
	console.log(this); //expecting to see object c, but instead points to the global object
};

//fix
var c = {
	var that = this;

	that.name: 'Updated c object';
	console.log(that); //c object

	var setname = function (newname) {
		that.name = newname;
	}

	setname('Updated again! The c object');
	console.log(that); //will expect to see c object
};
```


### Lecture 38 - Arrays ###
```javascript
var arr = [
	1,
	false,
	{
		name: 'John',
		...
	},
	function (name) {
		var greeting = 'Hello ';
		console.log(greeting + name);
	},
	"hello"
];

arr[3](arr[2].name); //invoke a function in an array
```

### Lecture 39 - 'arguments' and spread ###
`arguments` output a list of all the values of the parameters (deprecated in ES6)

```javascript
//example of spread
//anything after the first 2 parameters will be stored in an array called other
function greet(firstname, lastname, ...other) {
	...
}

greet('John', 'Smith', '111 Main St', 'New York');
```


### Lecture 40 - Framework Aside: Function Overloading ###
No function overloading in JS

```javascript
//Simple example of overloading a function
function greet(firstname, lastname, language) {
	...
}

function greetEn(firstname, lastname) {
	greet(firstname, lastname, 'en');
}

function greetEs(firstname, lastname) {
	greet(firstname, lastname, 'es');
}

greetEn('John', 'Smith'); //rather than greet('John', 'Smith', 'en');
greetEs('Jose', 'Smith'); //rather than greet('Jose', 'Smith', 'es');
```


### Lecture 44 - Immediately Invoked Functions Expressions (IIFEs) ###
```javascript
//function statement
function greet(name) {
	...
}
greet();

//using a function expression
var greetFunc = function (name) {
	...
};
greetFunc();

//Immediately Invoked Function Expression (IIFE)
var greeting = function (name) {
	...
}('John'); //IIFE with name

//IIFE without having a variable, you use wrap it with ()
//so that it does not error, because when the engine finds the word 'function' it expects a name
(function (name) {
	...
}('John')); //IIFE without name

```


### Lecture 46 - Understanding Closures ###
![Closures](http://robinjulius.com/wp-content/uploads/2015/12/44-01-1024x510.png)

In the above example, even though the greet function is finished, any functions created inside will still have a reference to the outer function's (greet()) execution context

The Javascript engine will make sure that the function will always have access to the variables that it's supposed to. Making sure the scope is intact


### Lecture 47 - Understanding Closures - Part 2 ###
```javascript
function buildFunctions() {
	var arr = [];

	for (var i = 0; i < 3; i++) {
		arr.push(function () {
			console.log(i);
		});
	}

	return arr;
}

var fs = buildFunctions();
fs[0](); //3
fs[1](); //3
fs[2](); //3

//ES6 fix
function buildFunctions2() {
	var arr = [];

	for (var i = 0; i < 3; i++) {
		let j = i //scoped to the block

		arr.push(function () {
			console.log(j);
		});
	}

	return arr;
}

var fs2 = buildFunctions2();
fs2[0](); //0
fs2[1](); //1
fs2[2](); //2

//ES5 and below fix
function buildFunctions3() {
	var arr = [];

	for (var i = 0; i < 3; i++) {
		arr.push(
			(function (j) {
				return function () {
					console.log(j);
				}
			}(i)); //IIFE
		);
	}

	return arr;
}

var fs3 = buildFunctions3();
fs3[0](); //0
fs3[1](); //1
fs3[2](); //2
```


### Lecture 49 - Closures and Callbacks ###
**Callback function:** a function you give to another function to be run when the first function is finished

```javascript
function tellMeWhenDone(callback) {
	...

	callback(); //the 'callback' runs the function given
}

//first callback
tellMeWhenDone(function () {
	console.log('Init callback');
});

//second callback
tellMeWhenDone(function () {
	console.log('Init callback a second time');
});
```



