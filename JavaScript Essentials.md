JavaScript Essentials
=====================

### Values

| Type      | Notes        |
|-----------|------------- |
| Numbers   | 42, 3.14159  |
| Boolean   | true / false |
| Strings   | "Howdy"      |
| null      | a special keyword denoting a null value. |
|undefined  | a top-level property whose value is undefined.|

JavaScript is a **dynamically typed** language. That means you don't have to specify the data type of a variable when you declare it, and data types are converted automatically as needed during script execution.

```JavaScript
var answer = 42;
answer = "Thanks";
```

In JavaScript, `undefined` means a variable has been declared but has *not yet been assigned a value*; while `null` is an assignment value. It can be assigned to a variable as *a representation of no value*.

`undefined` and `null` are two distinct types: `undefined` is a type itself (undefined) while `null` is an object.

```JavaScript
var variable          // undefined variable
typeof variable       // undefined
```

```JavaScript
var variable = null   // null variable
typeof variable       // object
```


### Arrays

The following example creates the coffees array with three elements and a length of three:

```JavaScript
var coffees = ["French Roast", "Colombian", "Kona"];
```

The following example creates the fish array, which has two elements with values and one empty element (`fish[0]` is `"Lion"`, `fish[1]` is `undefined`, and `fish[2]` is `"Angel"`):

```JavaScript
var fish = ["Lion", , "Angel"];
```

### Operators

#### Comparison operators

JavaScript has two sets of equality operators: `===` and `!==`, and `==` and `!=`. 

If the two operands are of *the same type and have the same value*, then `===` produces `true` and `!==` produces `false`, which behaves similarly to `==` in C++ or Java.

If the operands are of the same type, but if they are of different types, `==` and `!=` attempt to *coerce the values*. 

```JavaScript
'' == '0'           // false
0 == ''             // true
0 == '0'            // true

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```

As you see, the way JavaScript coerce the values is quite unpredictable. So a good practice is to **never** use `==` and `!=`. Instead, always use `===` and `!==`. 

#### _in_ operator

The `in` operator returns true if the specified property is in the specified object. The syntax is:

```JavaScript
propNameOrNumber in objectName
```

#### _instanceof_ operator


The `instanceof` operator returns true if the specified object is of the specified object type. The syntax is:

```JavaScript
objectName instanceof objectType
```

#### _void_ operator

The `void` operator specifies an expression *to be evaluated without returning a value*. expression is a JavaScript expression to evaluate. 

```JavaScript
<A HREF="javascript:void(document.form.submit())">Submit</A>
```

### Regular Expressions

You construct a regular expression in one of two ways:

Using a regular expression literal, as follows:

```JavaScript
var re = /ab+c/;
```

Calling the constructor function of the RegExp object, as follows:

```JavaScript
var re = new RegExp("ab+c");
```

Regulation expressions are used with the `exec` and `test` methods of `RegExp`, and with the `match`, `replace`, `search`, and `split` methods of `String`. 

### Statements

#### _for...in_ loop

```JavaScript
for (variable in object) {
   statements
}
```

#### _throw_ Statement

Just about any object can be thrown in JavaScript. 

```JavaScript
throw "Error";    //String type
throw 42;         //Number type
throw true;       //Boolean type
throw {toString: function() { return "I'm an object!"; } };
```

### Functions

Just like other languages, a function in JavaScript is a set of statements that performs a task or calculates a value. However, JavaScript functions are used in much more flexible ways than languages like C# or Java.

This section will list some of the common usages of JavaScript functions. Some of them are probably not so clear at this time. But they will be clear after we finish talking about JavaScript objects.

#### Defining Functions

There are several ways to define a function:

**Function declaration**

Traditional way of declare a function in the current scope:

```JavaScript
function foo(){}
```

**Function expression**

Functions are also objects, so they can be assigned to variables just like other objects. The following code define an *anonymous function* and assign it to a variable:

```JavaScript
var fn = function(){}
```

> It is important to distinguish between **function declarations** and **function expressions**. Function declarations loads before any code is executed. While function expressions loads only when the interpreter reaches that line of code.

**Named function expression**

The function assigned to a variable can be anonymous or named.

```JavaScript
var fn = function foo(){}
```

The function name is only accessible within the function. If you want to use recursion, this is probably the way to go. 

Using named function expressions helps in debugging, since the function name shows up on the call stack.

**Function constructor**

Use `Function` as a constructor to define a function:

```JavaScript
var F = new Function('arg1', 'arg2', 'console.log(arg1 + ", " + arg2)');
F('foo', 'bar');  // Console output: 'foo, bar'
```

Or directly call `Function` to get the same result:

```JavaScript
var F = Function('arg1', 'arg2', 'console.log(arg1 + ", " + arg2)');
F('foo', 'bar');  // Console output: 'foo, bar'
```

> Note: `function` and `Function` are completely different. `function` is a JavaScript keyword, while `Function` is a built-in function.

We will talk about constructors later.


#### Calling Functions

While there are different ways defining a function, there are also several different ways calling a function.

Suppose we have a function defined:

```JavaScript
function makeArray(arg1, arg2){  
    return [ this, arg1, arg2 ];  
}  
```

**Direct calls**

```JavaScript
makeArray('one', 'two');  //  [ window, 'one', 'two' ]  
```

Since we call it in the global scope, `this` is `window` here.

**Use apply() and call()**

```JavaScript
var gasGuzzler = {year: 2008, model: 'Dodge Bailout'};  
makeArray.apply(gasGuzzler, [ 'one', 'two' ]);  // [ gasGuzzler, 'one' , 'two' ]  
makeArray.call(gasGuzzler,  'one', 'two');      // [ gasGuzzler, 'one' , 'two' ]  
```

The first parameter will override `this`. 

>`apply()` and `call()` differ on the subsequent arguments. 
>`Function.apply()` takes an array of values that will be passed as arguments to the function.
>`Function.call()` takes the same arguments separately.


**Immediately-invoked function expressions (IIFE)**

The function defined below gets invoked immediately.

```JavaScript
var output = (function(){
  return 'bar';
})(); // output is 'bar'
```

**Used as object constructor**

```JavaScript
var obj = new function(){};
```

What this line of code does is use an anonymous function as a constructor to construct a new object. While the function being executed, an new object is created. See Section Objects for more information.

#### Arguments

The arguments of a function are maintained in an array-like object. Within a function, you can address the arguments passed to it as follows:

```JavaScript
arguments[i]
```

where `i` is the ordinal number of the argument.

An example of using `arguments` array:

```JavaScript
function myConcat(separator) {
   var result = "", i;
   // iterate through arguments
   for (i = 1; i < arguments.length; i++) {
      result += arguments[i] + separator;
   }
   return result;
}
```

You can pass any number of arguments to this function, and it concatenates each argument into a string array:

```JavaScript
// returns "red, orange, blue, "
myConcat(", ", "red", "orange", "blue");

// returns "elephant; giraffe; lion; cheetah; "
myConcat("; ", "elephant", "giraffe", "lion", "cheetah");

// returns "sage. basil. oregano. pepper. parsley. "
myConcat(". ", "sage", "basil", "oregano", "pepper", "parsley");
```

### Objects

JavaScript is an object-based language. Everything in JavaScript is an object.

An object is a collection of properties; and a property is just a key-value pair. So everything in an object are just **key-value pairs** -- both variables and functions.

#### Properties

Add properties to an object with a simple *dot-notation*:

```JavaScript
var myCar = new Object();
myCar.make = "Ford";
myCar.model = "Mustang";
myCar.year = 1969;
```

Objects are sometimes called *associative arrays*. Properties of JavaScript objects can also be accessed or set using a *bracket notation*.

```JavaScript
myCar["make"] = "Ford";
myCar["model"] = "Mustang";
myCar["year"] = 1969;
```

There are three native ways to list/traverse object properties:

* `for...in` loops
    This method traverses all enumerable properties of an object and its prototype chain.
* `Object.keys(o)`
    This method returns an array with all the own (not in the prototype chain) enumerable properties' names of an object `o`.
* `Object.getOwnPropertyNames(o)`
    This method returns an array containing all own properties' names (enumerable or not) of an object `o`.

#### Creating New Objects

There several ways to create custom objects in JavaScript:

**Using object initializers**

```JavaScript
var obj = { property_1:   value_1,   // property_# may be an identifier...
            2:            value_2,   // or a number...
            // ...,
            "property n": value_n }; // or a string
```

**Using a constructor function**

```JavaScript
function Car(make, model, year) {
  this.make = make;
  this.model = model;
  this.year = year;
}
var mycar = new Car("Eagle", "Talon TSi", 1993);
```

This is perhaps a little bit difficult to understand for class-based language developers. The so-called constructors in JavaScript is quite different from constructors in languages like C++ or Java. 

*In JavaScript a constructor is just a function that happens to appear after a `new` keyword*. 

When JavaScript sees an `new` keyword, it creates an new object, and executes the function after the `new` keyword, all variables referenced by `this` within the function are regarded as properties of the new object. 

The `new` keyword is not followed by a class type, but a function, and returns an object. This process will be discussed in detail later.

**Using the Object.create method**

Objects can also be created using the Object.create method. This method can be very useful, because it allows you to choose the prototype object for the object you want to create, without having to define a constructor function. 

```JavaScript
// Animal properties and method encapsulation
var Animal = {
  type: "Invertebrates", // Default value of properties
  displayType : function(){  // Method which will display type of Animal
    console.log(this.type);
  }
}

// Create new animal type called animal1 
var animal1 = Object.create(Animal);
animal1.displayType(); // Output:Invertebrates

// Create new animal type called Fishes
var fish = Object.create(Animal);
fish.type = "Fishes";
fish.displayType(); // Output:Fishes
```

#### Prototypes

JavaScript is an object-based language based on prototypes, rather than being class-based. So in JavaScript, there is no class or instance: it simply has objects. 

A prototype-based language has the notion of a *prototypical object*, an object used as a template from which to get the initial properties for a new object. 

Any object can specify its own properties, either when you create it or at run time. In addition, any object can be associated as the *prototype* for another object, allowing the second object to share the first object's properties.

**___proto___ property**

`__proto__` is an internal property of an object, pointing to its prototype (its *parent* object). Sometimes, we use *[[prototype]]* instead of `__proto__`, but it is just a notation, they mean exactly the same thing.

Since everything in JavaScript is an object, every object's *[[prototype]]* eventually points to JavaScript's built-in `Object`, i.e. every object is a child of `Object`. And `Object` has `null` as its *[[prototype]]*. For example:

```JavaScript
var obj = new Object();   // [[prototype]] chain: obj -> Object -> null
var str = "Hello World!"; // Strings are objects: str -> String -> Object -> null
var fn  = function (){};  // Functions are also objects: fn -> Function -> Object -> null
```

JavaScript has some predefined objects, such as `Boolean`,`String`,`Number`,`Function`,`Array`,`Date`, etc. 

When you look up a property via `obj.propName` or `obj['propName']` and the object does not have such a property, the runtime looks up the property in the object referenced by *[[Prototype]]* instead. If the prototype-object also doesn't have such a property, its *[[Prototype]]* is checked in turn, thus walking the original object's prototype-chain until a match is found or its end is reached.

In this way every object *inherits* its prototype's properties. So you can see every object has a property `toString()` (remember method is also property) inherited from `Object`.

**_prototype_ property**

It is quite confusing in JavaScript that some objects have a `prototype` property along with `__proto__` property. So what is the difference?

As we have discussed above, every object has a `__proto__` object, and it is the actual object that is used in the lookup chain to resolve methods. 

While `prototype` is a special property of a `Function` object. It is the prototype of objects constructed by that function.

When we create a new object from a constructor function:

```JavaScript
var obj = new Foo();
```

What JavaScript does when it sees the `new` keyword is:

1. It creates a new object. The type of this object, is simply `Object`.
2. It sets this new object's internal *[[prototype]]* property to be the constructor function's *prototype* object (pointed by the *prototype* property).
3. It executes the constructor function, using the newly created object whenever `this` is mentioned.
4. It returns the newly created object, unless the constructor function returns a non-primitive value. In this case, that non-primitive value will be returned.

This is how an object is created from a function and how the *prototype* works.

Lets see an example of using *prototype*:

Define a constructor function `Employee`. From the procedure above, we know `this` is the newly created object when we execute the constructor function. That's why we can use `this` to define properties in the new object.

```JavaScript
function Employee () {
  this.name = "";
  this.dept = "";
}
```

Define another constructor function `Manager` and set its `prototype` property to an object created by `Employee`.

```JavaScript
function Manager () {
  this.reports = [];
}
Manager.prototype = new Employee;
```

When we create a new object using `Manager` function:

```JavaScript
var mgr = new Manager();
```

JavaScript sets the internal *[[prototype]]* of `mgr` to be the `prototype` of `Manager`, i.e. `mgr.__proto__ = Manager.prototype`. 

`Manager.prototype` is an object with properties `name` and `dept`. In this way, `mgr` *inherits* the properties `name` and `dept` from its prototype object. 

> Notice that when you then access properties of an instance, JavaScript first checks whether they exist on that object directly, and if not, it looks in its *[[Prototype]]*, which is defined in its constructor's *prototype* property . This means if you change a constructor function's *prototype*, the change is effectively *shared by all instances* (objects created from that function). You can even later change parts of *prototype* and have the changes appear in all existing instances, if you wanted to.

#### Objects and Functions

JavaScript has some *predefined objects*, such as `Boolean`,`String`,`Number`,`Function`,`Array`,`Date`, etc. But you never get access to these objects directly. The `Boolean`,`String` or `Number` you use in your code, are in fact, *predefined functions*.

```JavaScript
typeof Object   // function
typeof String   // function
typeof Function // function
```

You can use these predefined functions to create the corresponding objects.

```JavaScript
var obj = new Object();
typeof obj      // Object
```

These predefined functions has the corresponding objects as their *prototype*. For example, function `String()` has a `String` object as its `prototype`; function `Boolean()` has a `Boolean` object as its `prototype`.

```JavaScript
String.prototype  // [object String]
Boolean.prototype // [object Boolean]
```

Inversely, an object has a property called `constructor` indicating from which function it is created. `constructor` is a property defined in `Object`, and thus inherited by all objects. For example, a `String` object has a `constructor` function `String()`.

```JavaScript
str = new String("JavaScript");
str.constructor // function String()
```

A function itself is an object. A custom function you define uses predefined `Function` object as its *[[prototype]]*. Its `prototype` property, if not assigned, is the predefined object `Object` by default, which means the new object you create with that function will use `Object` as its template. As an object, a function itself has its constructor function, which is the function `Function()`. But again remember function `Function()` itself is still an object.


### Closures

A closure is a special kind of object that combines two things: a function, and the environment in which that function was created. 

A closure lets you associate some data (the environment) with a function that operates on that data. 

An example of a closure:

```JavaScript
function makeFunc() {
  var name = "JavaScript";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var func = makeFunc(); // func is a function
func();                // displays "JavaScript"
```

The `makeFunc` above is a closure, which encloses a method `displayName` and a string data `"JavaScript"`. 

The magic here is the `name` variable remains accessible even after `makeFunc` finishes executing. `makeFunc` finishes after we call `var func = makeFunc()`; however, variable `name` and its value still remains accessible when we call `func()`.

The solution to this puzzle is that `myFunc` has become a *closure*. It encloses both the methods and the variables defined inside it.

### Useful References

1. http://www.w3schools.com/js/
2. https://developer.mozilla.org/en-US/docs/Web/JavaScript


