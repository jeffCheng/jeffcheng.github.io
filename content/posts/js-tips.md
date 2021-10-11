---
title: "[Javascript] var, let, const, null, undefined, pass by value, pass by reference"
date: 2021-10-11T16:33:26+08:00
draft: false
---

## 1. var, let and , const？

`var`, `let` and `const` are very common to use in JavaScript programming. Especially, in Javascript's new feature ES2016.

## `Let`

The let statement declares a *block-scoped local variable*, optionally initializing it to a value.

### What is a Block-scoped?

Before ES6 (2015), JavaScript had only *Global Scope* and *Function Scope*.

ES6 introduced two important new JavaScript keywords: `let` and `const`.

These two keywords provide **Block Scope** in JavaScript.

Variables declared inside a `{ }` block cannot be accessed from outside the block:

```tsx


{
  let x = 3;
}
// x can NOT be used here


```

`let` allows you to declare variables that are limited to the scope of a block statement, or expression on which it is used, unlike the `var` keyword, which declares a variable *globally*, or *locally* to an entire function regardless of block scope.

```tsx


function varTest() {
  var x = 3;
  {
    var x = 3;  // same variable!
    console.log(x);  // 3
  }
  console.log(x);  // 3
}

function letTest() {
  let x = 2;
  {
    let x = 3;  // different variable
    console.log(x);  // 3
  }
  console.log(x);  // 2
}


```

At the top level of programs and functions, let, unlike var, does not create a property on the global object. For example:

```tsx


var x = 'global';
let y = 'global';
console.log(this.x); // "global"
console.log(this.y); // undefined


```

## `Const`

Constants are *block-scoped*, much like variables declared using the let keyword. The value of a constant can't be changed through reassignment, and it can't be redeclared.

```tsx


const number = 42;

try {
  number = 99;
} catch (err) {
  console.log(err);
  // expected output: TypeError: invalid assignment to const `number'
  // Note - error messages will vary depending on browser
}

console.log(number);
// expected output: 42


```

The const declaration creates a read-only reference to a value. It does not mean the value it holds is immutable—just that the variable identifier *cannot be reassigned*. For instance, in the case where the content is an object, this means the object's contents (e.g., its properties) can be altered.

```jsx


if (MY_FAV === 7) {
  // this is fine and creates a block scoped MY_FAV variable
  // (works equally well with let to declare a block scoped non const variable)
  let MY_FAV = 20;

  // MY_FAV is now 20
  console.log('my favorite number is ' + MY_FAV);

  // this gets hoisted into the global context and throws an error
  var MY_FAV = 20;
}

// MY_FAV is still 7
console.log('my favorite number is ' + MY_FAV);


```

### `const` needs to be initialized

```jsx


// throws an error
// Uncaught SyntaxError: Missing initializer in const declaration

const FOO;


```

### Scope of var: 

`var` declarations are globally scoped or function locally. The default value is undefined.
`var` declarations, wherever they occur, are processed before any code is executed. This is called hoisting and is discussed further below.

```jsx


var x = 1;

if (x === 1) {
  var x = 2;

  console.log(x);
  // expected output: 2
}

console.log(x);
// expected output: 2


```

## `Var`

The var statement declares a *function-scoped or globally-scoped* variable, optionally initializing it to a value.

```jsx


var x = 1;

if (x === 1) {
  var x = 2;

  console.log(x);
  // expected output: 2
}

console.log(x);
// expected output: 2


```

`var` declarations, wherever they occur, are processed before any code is executed. This is called *hoisting*, and is discussed further below.

The scope of a variable declared with `var` is its current *execution context and closures thereof*, which is either the enclosing function and functions declared within it, or, for variables declared outside any function, global. Duplicate variable declarations using `var` will not trigger an error, even in strict mode, and the variable will not lose its value, unless another assignment is performed.

Variables declared using var are created before any code is executed in a process known as hoisting. Their initial value is undefined.

### `var` problem:

`var` problems can be declared repeatedly, which is easy to cause confusion
Leaving the scope of `{}`, you can still get the value of var i

```jsx

for (var i = 0; i <10 ; i++) {
    console.log('hello');
}
console.log(i) // i=5

```

## 2. Pass by Value and Pass by Reference in Javascript

Pass By Value: In Pass by value, function is called by directly passing the value of the variable as an argument. So any changes made inside the function does not affect the original value.

```jsx

function Passbyvalue(a, b) {
    let tmp;
    tmp = b;
    b = a;
    a = tmp;
    console.log(`Inside Pass by value 
        function -> a = ${a} b = ${b}`);
}
  
let a = 1;
let b = 2;
console.log(`Before calling Pass by value 
        Function -> a = ${a} b = ${b}`);
  
Passbyvalue(a, b);
  
console.log(`After calling Pass by value 
       Function -> a =${a} b = ${b}`);

```

**Pass by Reference:** In Pass by Reference, Function is called by directly passing the reference/address of the variable as an argument. So changing the value inside the function also change the original value. In JavaScript **array and Object** follows pass by reference property.

In Pass by reference, parameters passed as an arguments does not create its own copy, it refers to the original value so changes made inside function affect the original value.

Note: In Pass by Reference, we are mutating the original value. when we pass an object as an arguments and update that object’s reference in the function’s context, that won’t affect the object value. But if we mutate the object internally, It will affect the object .

```jsx

function PassbyReference(obj) {
  
    // Changing the reference of the object
    obj = {
        a: 10,
        b: 20,
        c: "BEST"
    }
    console.log(`Inside Pass by 
        Reference Function -> obj `);
          
    console.log(obj);
}
  
let obj = {
    a: 10,
    b: 20
  
}
console.log(`Updating the object reference -> `)
console.log(`Before calling Pass By 
        Reference Function -> obj`);
console.log(obj);
  
PassbyReference(obj)
console.log(`After calling Pass By 
        Reference Function -> obj`);
console.log(obj);

```

## 3. The difference between undefined and null

### undefined

The global undefined property represents the primitive value undefined. It is one of JavaScript's primitive types.

### null

The value null is written with a literal: null. null is not an identifier for a property of the global object, like undefined can be. Instead, null expresses a lack of identification, indicating that a variable points to no object. In APIs, null is often retrieved in a place where an object can be expected but no object is relevant.

- **Null:** It is the intentional absence of the value. It is one of the primitive values of JavaScript.
- **Undefined:** It means the value does not exist in the compiler. It is the global object.

**Type:**

**Null:** Object

**Undefined:** undefined

```jsx

null == undefined // true
null === undefined // false

```

When we define a variable to *undefined* then we are trying to convey that the variable does not exist .When we define a variable to *null* then we are trying to convey that the variable is empty.

**Examples:**
- **Null:**
```jsx

null ? console.log("true") : console.log("false") // false 

```
        
*Null* is also referred as *false*.
- **Undefined:** When variable is not assigned a value
```jsx

var temp;
if(temp ===undefined)
console.log("true");
else
console.log("false"); 

```
**Output:**
```jsx

true

```
Accessing values which does not exist
```jsx

var temp=['a','b','c'];
if(temp[3] === undefined)
        console.log("true");
        else
        console.log("false");

```
**Output:**
```jsx

true

```
        
Resources:


[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)

[https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

[https://www.w3schools.com/js/js_scope.asp](https://www.w3schools.com/js/js_scope.asp)

[https://medium.com/@allansendagi/block-scope-in-javascript-8fd2f909e848](https://medium.com/@allansendagi/block-scope-in-javascript-8fd2f909e848)

[https://www.geeksforgeeks.org/undefined-vs-null-in-javascript/](https://www.geeksforgeeks.org/undefined-vs-null-in-javascript/)

[https://www.geeksforgeeks.org/pass-by-value-and-pass-by-reference-in-javascript/](https://www.geeksforgeeks.org/pass-by-value-and-pass-by-reference-in-javascript/)