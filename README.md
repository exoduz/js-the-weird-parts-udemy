# Javascript: The Weird Parts #
##### https://www.udemy.com/understand-javascript #####

### Contents ###
1. [Section 2 - Execution Contexts and Lexical Environments](#section-2)
	1. [Lecture 7 - Conceptual Aside: Name/Value Pairs and Objects](#lect-7)
	2. 
2. [Section 3 - Types and Operators](#section-3)
3. [Section 4 - Objects and Functions](#section-4)
4. [Section 5 - Object Oriented Javascript and Prototypal Inheritance](#section-5)
5. [Section 6 - Building Objects](#section-6)
6. [Section 7 - Odds and Ends](#section-7)
	1. [Lecture 65 - typeof, instanceof, and Figuring Out What Something Is](#lect-65)

<a id="section-2"></a>
## Section 2 - Execution Contexts and Lexical Environments ##

<a id="lect-7"></a>
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

<a id="lect-9"></a>
### Lecture 9 - The Global Environment and the Global Object ###
Execution context creates "Global Object (`window`)" and `this`  
`this` refers to the "window" object at the global level  
Global object means "not inside a function"

<a id="lect-10"></a>
### Lecture 10 - The Execution Context - Creation and Hoisting ###
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

<a id="lect-11"></a>
### Lecture 11 - Conceptual Aside: Javascript and 'undefined' ###
`undefined` is not just the word, it's a special value which means that the variable hasn't been set

**DO NOT** do `a = undefined`, let it mean "I, the programmer, never set it's value"

<a id="lect-13"></a>
### Lecture 13 - Conceptual Aside: Single Threaded, Synchronous Execution ###
**Single Threaded:** one command at a time  
**Synchronous:** one at a time, and in order

<a id="lect-14"></a>
### Lecture 14 - Function Invocation and the Execution Stack ###
**Invocation:** run/call the function  
**Execution Stack:** the order in which the functions in invoked. The more recent the function call, the higher it sits on the execution stack

![Execution Stack](https://robinjulius.com/blog/wp-content/uploads/2015/12/14-01-1024x700.png)

Every function creates a new execution context which runs through function line by line.

<a id="lect-16"></a>
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

----
<a id="section-3"></a>
## Section 3 - Types and Operators ##

<a id="lect-20"></a>
### Lecture 20 - Conceptual Aside: Primitive Types ###
**undefined** Lack of existence (you shouldn't set a variable to this), but you can test for it  
**null** Lack of existence (you can set a variable to this)  
**boolean** true / false  
**number** _floating point_  
**string** sequence of characters ('' and "" can be used)  
**symbol** only used in ES6

<a id="lect-22"></a>
### Lecture 22 - Operator Precedence and Associativity ###
[Operator Precedence and Associativity Table on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

**Associativity:** When 2 or more operators have the same precedence. Right to left or left to right, check the above link for more information

<a id="lect-24"></a>
### Lecture 24 - Conceptual Aside: Coercion ###
**Coercion:** Converting a value from 1 type to another

```javascript
var a = 1 + '2'; //12
```
<a id="lect-25"></a>
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

<a id="lect-27"></a>
### Lecture 27 - Existence and Booleans ###
```javascript
Boolean(undefined); //false
Boolean(null); //false
Boolean(''); //false
Boolean(0); //false
```
----
<a id="section-4"></a>
## Section 4 - Objects and Functions ##

<a id="lect-30"></a>
### Lecture 30 - Objects and the Dot ###
![Objects](https://robinjulius.com/blog/wp-content/uploads/2015/12/30-01-1024x660.png)

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

<a id="lect-31"></a>
### Lecture 31 - Objects and Object Literals ###
**Object Literal:** short hand of declaring variables `var person = {};` instead of `var person = new Object();`

<a id="lect-32"></a>
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

<a id="lect-33"></a>
### Lecture 33 - JSON and Object Literals ###
`JSON.stringify()` - convert to JSON  
`JSON.parse()` - convert to JS object

<a id="lect-34"></a>
### Lecture 34 - Functions are Objects ###
Function **names** are optional  
**Functions are Objects**

<a id="lect-35"></a>
### Lecture 35 - Function Statements and Function Expressions ###
**Expression:** Code that results in a value

```javascript
//function statement
function greet() {
	console.log('hello');
}
greet(); //invoke function, result is 'hello'

//function expression
var anonymousGreet = function() {
	console.log('hi');
}
anonymousGreet(); //invoke anonymous function, result is 'hi'

function log(a) {
	console.log(a); //will just output a string of the anonymous function below
}
log(3); //3

function log2(a) {
	a(); //run a function that is passed as a parameter, result is 'hi'
}

log2(function() {
	console.log('hi');
});
```

<a id="lect-36"></a>
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

console.log(c); //hello
console.log(d); //hello

//equals operator sets up new memory space (new address)
c = { greeting: 'howdy' };
console.log(c); //howdy
console.log(d); //hello
```

<a id="lect-37"></a>
### Lecture 37 - Objects, Functions and 'this' ###
```javascript
function a() {
	console.log(this);
}

var b = function() {
	console.log(this);
}

a(); //this is global object
b(); //this is global object

var c = {
	name: 'The c object',
	log: function() {
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

<a id="lect-38"></a>
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

<a id="lect-39"></a>
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

<a id="lect-40"></a>
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

<a id="lect-44"></a>
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

<a id="lect-46"></a>
### Lecture 46 - Understanding Closures ###
![Closures](https://robinjulius.com/blog/wp-content/uploads/2015/12/44-01-1024x510.png)

In the above example, even though the greet function is finished, any functions created inside will still have a reference to the outer function's (greet()) execution context

The Javascript engine will make sure that the function will always have access to the variables that it's supposed to. Making sure the scope is intact

<a id="lect-47"></a>
### Lecture 47 - Understanding Closures - Part 2 ###
```javascript
function buildFunctions() {
	var arr = [];

	for (var i = 0; i < 3; i++) {
		arr.push(function() {
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

		arr.push(function() {
			console.log(j);
		});
	}

	return arr;
}

var fs2 = buildFunctions2();
fs2[0](); //0
fs2[1](); //1
fs2[2](); //2
// this is like asking a child what age the father is now, and not what age he had each one of this children


//ES5 and below fix
function buildFunctions3() {
	var arr = [];

	for (var i = 0; i < 3; i++) {
		arr.push(
			(function (j) {
				return function() {
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

<a id="lect-49"></a>
### Lecture 49 - Closures and Callbacks ###
**Callback function:** a function you give to another function to be run when the first function is finished

```javascript
function tellMeWhenDone(callback) {
	...
	callback(); //the 'callback' runs the function given
}

//first callback
tellMeWhenDone(function() {
	console.log('Init callback');
});

//second callback
tellMeWhenDone(function() {
	console.log('Init callback a second time');
});
```

<a id="lect-50"></a>
### Lecture 50 - call(), apply() and bind() ###
All functions have access to `call()`, `apply()` and `bind()`  
These 3 functions have something to do with the `this` variable

`bind()` creates a copy of the function, and takes what should be `this` as the 1st parameter  
Also allows you to set default parameters, the 2nd parameter of `bind()` is the 1st parameter of the function it is bound to, 3rd parameter is 2nd, etc...

`call()` invokes function/method, but does not create a copy like `bind()`, instead it executes the function  
1st parameter is what `this` should point to, the rest is the parameters you would pass to the function

`apply()` same as `call()` but wants an array as parameters

```javascript
var person = {
	firstname: 'John',
	lastname: 'Doe',
	getFullName: function() {
		var fullname = this.firstname + ' ' + this.lastname;
		return fullname;
	}
};

var logName = function (lang1, lang2) {
	console.log('Logged: ' + this.getFullName());
	console.log('Arguments: ' + lang1 + ' ' + lang2);
}

logName(); //running this alone would error because 'this' is only operated within the scope of the block, and would not find this.getFullName

var logPersonName = logName.bind(person); //allows 'person' object to be passed to the function and used as 'this'
logPersonName();

logName.call(person, 'en'. 'es'); //equivalent to logName() to invoke function, 1st param is what 'this' should point to

logName.apply(person, ['en', 'es']); //equivalent to above but requires an array as the parameters for the original function

//function borrowing
var person2 = {
	firstname: 'Jane',
	lastname: 'Doe'
	//no getFullName method
}

person.getFullName.apply(person2); //borrow it from 'person' object

//function currying
function multiply(a, b) {
	return a * b;
}

var multiplyByTwo = multiply.bind(this, 2); //2nd parameter replaces 'a' parameter permanently
multiplyByTwo(4); //only requires 'b' parameter, result is 8
```

**Function Currying:** creating a copy of a function but with some preset parameters

<a id="lect-51"></a>
### Lecture 51 - Functional Programming ###
Try not to mutate data  
If you need to mutate data, do it as high up the chain as possible  
Better yet, do not change the data but return something new

<a id="section-5"></a>
## Section 5 - Object Oriented Javascript and Prototypal Inheritance ##

<a id="lect-53"></a>
### Lecture 53 - Conceptual Aside: Classical vs Prototypal Inheritance ###
**Inheritance:** one object gets access to the properties and methods of another object

<a id="section-6"></a>
## Section 6 - Building Objects ##

<a id="lect-58"></a>
### Lecture 58 - Function Constructors and '.prorotype' ###
Capitalise first character of a class

```javascript
function Person(firstname, lastname) {
	this.firstname = firstname;
	this.lastname = lastname;
	//Do prototype instead of creating method here (this.getFullName = function() {...})
}

Person.prototype.getFullName = function() {
	return this.firstname + ' ' + this.lastname;
}

Person.prototype.getFormalFullName = function() {
	return this.lastname + ', ' + this.firstname;
}

var john = new Person('John', 'Doe');
console.log(john); //Person { firstname: "John", lastname: "Doe", getFullName: function... }
```

Why use prototype rather than create a new method in the Person class?  
If you create a method then it will take up memory space, 1000 Person objects means 1000 getFullName methods  
If you add it to the prototype then you would only have 1, even if you have 1000 objects

You need properties for each object (e.g. this.firstname) because you need different values per object, but methods (e.g. getFullName), you only need one

<a id="lect-60"></a>
### Lecture 60 - Conceptual Aside: Built-In Function Constructors ###
Function constructors `var a = new String("John")` create objects that contain primitives and methods in the String function (`indexOf`, `concat`, etc.), or whatever you create `new` (e.g. `Date`, `Number`, etc.)

```javascript
//extends String prototype with new method
String.prototype.isLengthGreaterThan = function(limit) {
	return this.length > limit;
}

console.log("John".isLengthGreaterThan(3));
```

<a id="lect-61"></a>
### Lecture 61 - Dangerous Aside: Built-In Function Constructors ###
**DO NOT** use built-in function constructors for primitives

```javascript
var a = 3 //primitive
var b = new Number(3); //object created with a built-in function contstructor

a == b; //true
a === b; //false
```

<a id="lect-62"></a>
### Lecture 62 - Dangerous Aside: Arrays and for...in ###
```javascript
Array.prototype.myCustomFeature = 'cool!';

var arr = ['John', 'Jane', 'Jim'];

for (var prop in arr) {
	//arrays in js are objects and you will iterate through the prototype as well
	console.log(prop + ': ' + arr[prop]); //result 0: John, 1: Jane, 2: Jim, myCustomFeature: cool!
}

for (i = 0; i < arr.length; i++) { ... } //use normal for loop instead
```

<a id="lect-63"></a>
### Lecture 63 - Object.create and Pure Prototypal Inheritance ###
Function constructors try to mimic classes

```javascript
//prototypal inheritance example
var person = {
	firstname: 'Default',
	lastname: 'Default',
	greet: function() {
		return 'Hi ' + this.firstname;
	}
};

var john = Object.create(person);
john.firstname = 'John';
john.lastname = 'Doe';
console.log(john); // Object {firstname: "John", lastname: "Doe", greet: function}
```

**Polyfill:** code that adds feature which older browser or engines __may__ lack

<a id="section-7"></a>
## Section 7 - Odds and Ends ##

<a id="lect-65"></a>
### Lecture 65 - typeof, instanceof, and Figuring Out What Something Is ###
`typeof` what type an instance is

```javascript
var b = "Hello"; //typeof b is String
var c = {}; //typeof c is Object

var d = []; //typeof d is Object, which is incorrect
Object.prototype.toString.call(d); //[Object array]
```

`instanceOf` returns true/false if any objects down the prototype chain contans this type of object

```javascript
function Person(name) { ... }
console.log(typeof e); //object
console.log(e instanceOf Person); //true, because e is an instance of Person
```

`typeof null` result is object, this is a **BUG** in JS
