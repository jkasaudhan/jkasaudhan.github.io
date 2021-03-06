---
layout: post
title: Weird parts of JavaScript?
subtitle: Collection of code snippets whose result looks unusual
---

Just to understand how JS works, I have been trying to make a list of JS code snippets whose output looks unusual to me. 
I am aware that, this is how JS works but it makes me feel weird about JS. Please let me know if you have figured out something like this, through the comment section below. It might be useful to debug our own code :)

### Data type of not a number is a number
When we try to get the type of NaN i.e not a number, it says typeof(NaN) is of number data type which is wierd in one way.

```javascript
  console.log(typeof(NaN)); //prints number
```

### Following behaviour is because of typeof(NaN) => number

```javascript
  console.log(angular.isNumber(parseInt('ee')));//prints true
```

### Type of null is an object

```javascript
  console.log(typeof(null)); //prints object
```

### angular.isDefined(NaN) => returns true

### angular.isDefined(NaN) => returns true

### angular.isDefined(null) => returns true

### console.log(NaN === NaN);  // logs "false"

### console.log(isNaN('jiten')) => prints true (Instead use Number.isNaN('jiten') => returns false to check if it is number)

### Initially it feels wierd to see the output of the following code

```javascript
  function createFunctions() {
    var funcArray = [];
    for(var i=0; i< 4; i++) {
      funcArray.push(function() {
        console.log(i);
      });
  }
    return funcArray;
  }

  var funcList = createFunctions();
  funcList[0](); // prints 4
  funcList[1](); // prints 4
  funcList[2](); // prints 4
  funcList[3](); // prints 4
```
Eventhough we might expect it to print 0, 1, 2, 3 at first glance, it actually prints 4, 4, 4, 4. This is how JS works and is related to closure. I have separate post explaining how environment variables are executed in the execution context stack in this particular case.

### Looks wierd how 'this' object works ?

```javascript
function globalFunction() {
console.log(this);
}

//call global function
globalFunction(); //prints global Window object

var grandFather = {
  message: "I am your grand father.",
  //direct method inside an object grandFather 
  setMessage: function() {
      console.log("Inside grand father's setMessage: ", this.message);
      console.log("Inside setMessage of grandFather: ", this);

      var changeMessage = function() {
         //feels unsual to print global Window object in changeMessage method. Here, this object points to global Window object not      //grandFather object
          console.log("Inside inner method of grandFather i.e inside changeMessage: ", this);
      }

      changeMessage();
  },

  //creating new object father
  father: {
    message: "I am your father.",
    setMessage: function() {
        console.log("Inside father's setMessage: ", this.message);
        console.log("Inside father's setMessage: ", this);
    }

  }
}

grandFather.setMessage();
grandFather.father.setMessage();
```
Just wait for a moment and try to think about the expected results :). Try to focus on the 'this' object inside `changeMessage()`, what do you expect? For me it feels weird because 'this' object inside `changeMessage()` method points to global Window object. I have separate post on how 'this' object works.

Prints following result:-

Window {external: Object, chrome: Object, document: document, Prototype: Object, Class: Object…}

Inside grand father's setMessage:  I am your grand father.

Inside setMessage of grandFather:  Object {message: "I am your grand father.", father: Object}

Inside inner method of grandFather i.e inside changeMessage:  Window {external: Object, chrome: Object, document: document, Prototype: Object, Class: Object…} //feels unsual to print global Window object in changeMessage method. Here, 'this' object points to global Window object but not grandFather object

Inside father's setMessage:  I am your father.

Inside father's setMessage:  Object {message: "I am your father."}

### Invoke function before it is declared ?
Unlike other programming languages like C# or JAVA, it is not mandatory to declare or define functions before invoking it.

```javascript
  //function invokation before declaring it.
  printName(); 
  
  function printName() { 
    console.log("I am Jack Sparrow");
  }
```

We might expect it to throw an error because we are calling `printName()` function before its body is defined. But, it is not the case in JS. This is because of [Hoisting](/2016-12-08-js-execution-behaviour)

### Logically 1 < 2 < 3 and 3 > 2 > 1 should return true but it is not the case.

```javasctipt
  console.log(1 < 2 < 3);//returns true
  console.log(3 > 2 > 1); // returns false
```

To understand this behaviour we should understand the [associativity of the operators in JS](http://www.scriptingmaster.com/javascript/operator-precedence.asp). <, <= and > ,>= has associativity from left to right which means JS enginee evaluates expressions from left to right. In case of  `1 < 2 < 3`, `1 < 2` is evaluated first which is true. And on second step,`true < 3 `is evaluated. Because of coercion, value of true becomes 1 and `1 < 3` is evaluated, which means true and finally the overall result becomes true.

Similarly, in case of `3 > 2 > 1`, `3 > 2` is evaluated first as true and on second step `true > 1` is evaluated. Because of automatic coercion value of boolean true becomes 1 and `1 > 1` is evaluated, which is false.

### [ ] == ![ ] => returns true
Try to log `console.log([] == ![])` How can an empty array be equal to its negation? Well, to understand this we should understand [operator precendence](http://www.scriptingmaster.com/javascript/operator-precedence.asp) and coercion in JS. In this case, negation operator(!) has higher precedence than comparasion (==) operator, which means `![]` is evaluated first which results `false`.Similarly, JS enginee coerces an empty array to value 0 in this case (try to log, [] == 0 => returns true) which means `0` == `false`, false is coerced as a 0 value therefore `0 == 0` becomes true.

### Inconsistent addition of object

```javascript
  // type following in console of developer's tool
  
  [] + {}; // prints [object object]
  console.log([] + {}); //prints [object object]
  
  But, 
  {} + []; //prints 0
  and 
  console.log({} + []); //prints [object object]
  
```

### JSON.stringify(-0) and String(-0) returns string zero without minus "0"

### Number(undefined) returns NaN but Number(null) returns 0

### Number([]) returns 0 but Number({}) returns "[object object]"

### String([]) returns "" but String({}) returns "[object object]"

### String(null) returns "null" which looks fine but String([null]) returns empty string ""

### String(undefined) returns "undefined" which looks fine but String([undefined]) returns empty string ""

### String([null,null,]), String([undefined,undefined,]), String([,,]) returns ","

