# JS--React-Note

## The story behind Let, Const & Var
[Article Link](https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/)

Understanding var, let, and const in ```Scope, Reassigning and Accessing the variables```

### Scope:
In JavaScript, we use scope as a way to identify where and whether we can use the respective declared variable. The variables may exist within a block, inside a function, or outside a function and block.

Their are 3 types of Scope:
1) Block: <br>
If you do not want a variable declared inside a { } block to be accessed outside of the block, you need to declare them using the let or const keywords. Variables declared with the var keyword inside the { } block are accessible outside of the block too. So, be careful.

```
{
    let f_name  = 'Alex';
    const ZIP = 500067;
    var age = 25;
}

console.log(f_name); // Uncaught ReferenceError: f_name is not defined
console.log(ZIP);  // Uncaught ReferenceError: ZIP is not defined
console.log(age);  // 25
```
The value of the age variable may get overridden unknowingly and eventually introduce a bug. So, do not use the var keyword inside a block (block scope). Always use let and const instead.

2) Functional: <br>
A variable declared inside a function using these keywords is not accessible outside the function. That's the applied functional scope.

```
function f1() {
 let f_name = "Alex";
 const ZIP = 560089;
 var age = 25;   
}

f1();

console.log(f_name); // Uncaught ReferenceError: f_name is not defined
console.log(ZIP);  // Uncaught ReferenceError: ZIP is not defined
console.log(age);  // Uncaught ReferenceError: age is not defined
```
None of the variables are accessible outside of the function, not even age which is declared using var. So, the conclusion is, The variable declared with var inside a function is not accessible outside of it. The keyword var has function-scope.

3) Global: <br>

Variables declared outside of any functions and blocks are global and are said to have Global Scope. This means you can access them from any part of the current JavaScript program. 
```
let f_name = "Alex";
 const ZIP = 560089;
 var age = 25;  

// f1() is a function
function f1() {
  console.log(f_name); // Alex
  console.log(ZIP);  // 560089
  console.log(age);  // 25
}

f1();

console.log(f_name); // Alex
console.log(ZIP);  // 560089
console.log(age);  // 25
```
These variables are accessible everywhere.

### Reassign
Once you've declared a variable with var or let, you can reassign a new value to the variable in your programming flow. It is possible if the variable is accessible to assign a value. But with const, you can't reassign a new value at all.

```
// Declare variables with initial values
let f_name = "Alex";
const ZIP = 560089;
var age = 25;

// Reassign values
f_name = "Bob"; // the f_name value is 'Bob"
ZIP = 65457; // Uncaught TypeError: Assignment to constant variable.
age = 78; // the age value is 78
```

The tricky part with const is that once a variable is assigned with const you can still change its properties but you cannot reassign another value with the same variable.

```
const blog = {
    'url': 'https://greenroots.info'
}

blog.url = 'https://blog.greenroots.info"; //Allowed

blog = {}; // Uncaught TypeError: Assignment to constant variable.
```

### Accessing
You should never try accessing a variable without declaring it. But in case it happens, let's see how the variable may behave.

With var in non-strict mode, the variable will have an undefined value. This means that a variable has been declared but has no value assigned.
With let and const, if you try to access a variable before declaring, you will always get a ReferenceError. 
With let and const, if you try to access a variable before declaring, you will always get a ReferenceError.

### Summary:<br>
1) Don't use var anymore.
2) Use let or const.
3) Use const more often. Use let when you need to reassign another value to a variable. 
4) Don't try to access a variable without declaring it

## Template Literal & Tagged Template Literal
Before ES6(ECMAScript 2015), we have used single quotes('...') and double quotes("...") to wrap string literals.
There were limitations when we had to concatenate multiple strings and the string literal has dynamic values. The readability of these concatenations used to be a challenge as well.
```
var frag1 = "Hello, I'm";
var val1= "Joe";
var frag2 = "and my favorite color is";
var val2 = "purple";

var msg = frag1 + ' ' + val1 + ' ' + frag2 + ' ' + val2;
```

Template literals can contain placeholders that are specified by the dollar sign($) and curly braces(${expression}). The above example can be written with template literals as,

```
const name = 'Joe';
const color = 'purple';

const message = `Hello, I'm ${name} and my favorite color is ${color}`;
console.log(message);
```
Output: Hello, I'm Joe and my favorite color is purple.

### Tagged Template Literal
A Tagged Template Literal is usually a function that comes before a template literal to help you in manipulating the output.








