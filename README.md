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
[Article Link](https://blog.greenroots.info/what-exactly-is-javascript-tagged-template-literal)<br>
[Wesbos Article](https://wesbos.com/tagged-template-literals)

Also, something as ```Styled Components``` implmented in React.

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

Let us take an example of this template literal again,

`Hello, I'm ${name} and my favorite color is ${color}`

We want to manipulate the output such that, it returns a string like the below when we pass the name as, Joe and color as, green.

Hello Joe, Have a Nice Day! We know your favorite color is green

How about, displaying this message in the color that is passed as an expression to the template literal? Like this when the color value is green.

So, to do this there comes the power of Tag function:

### Tag Function:<br>

Let us first create a tag function. This is a regular JavaScript function that should return a value as per your needs. This return value is usually a manipulated output based on the template literal strings and expressions.
```function introduce() {                
    return 'introduce...';
}
```
Next, We mention the tag function before the template literal so that, the tag function gets associated with it.
```
const name = 'Joe';
const color = 'green';

const message = introduce`Hello, I'm ${name} and my favorite color is ${color}`;
```
Important, the tag function takes in arguments:

```
function introduce(strings, arg0, arg1) {
  console.log('strings', strings);
  console.log('arg0', arg0);
  console.log('arg1', arg1);

  return 'introduce...';
}

const name = 'Joe';
const color = 'purple';

const message = introduce`Hello, I'm ${name} and ${color} is my favorite color!`;
```
![image](https://user-images.githubusercontent.com/42742924/156871221-102e58fe-5fa4-474b-93f5-77de11d3f091.png)

But, passing an expression for each arguments is not a good idea as there can be as many as 10 expression or more. So, we use the concept of rest operators as shown in this example:

```function introduce(strings, ...values) {
  console.log('strings', strings);
  console.log('values', values);

  return 'introduce...';
}

const name = 'Joe';
const color = 'purple';

const message = introduce`Hello, I'm ${name} and ${color} is my favorite color!`;
```
![image](https://user-images.githubusercontent.com/42742924/156871331-c1e60928-9f1a-4382-a021-598f7062edce.png)

Now, we can manippulate these strings to get any desired output.

``` function introduce(strings, ...values) {                                                        
   let msg = 
     `<span style="color:${values[1]}">
           Hello ${values[0]}, Have a Nice Day! We know your favorite color is <u>${values[1]}</u>
      </span>`;

   return msg;
}

const name = 'Joe';
const color = 'green';

const message = introduce`Hello, I'm ${name} and ${color} is my favorite color!`;

console.log(message);
```

Output,
```
<span style="color:green">
    Hello Joe, Have a Nice Day! We know your favorite color is <u>green</u>
</span>
```

[React related Article](https://stackoverflow.com/questions/55119960/inserting-html-tags-in-template-literals-in-react)

## Arrow Functions
[Article Link](https://www.freecodecamp.org/news/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26/) <br>
Arrow functions (also called “fat arrow functions”) are undoubtedly one of the more popular features of ES6. They introduced a new way of writing concise functions.

```
function timesTwo(params) {  
    return params * 2}
}
timesTwo(4);  // 8
```

```
var timesTwo = params => params * 2
timesTwo(4);  // 8
```

### Variations in Arrow Functions
1) No Parameter:<br>
If there are no parameters, you can place an empty parentheses before
```() => 42```

2) Single Parameter:<br> 
With these functions, parentheses are optional:
```
x => 42  || (x) => 42
```

3) Multiple Parameter:<br>
Parentheses are required for these functions:
```(x, y) => 42```

4) Statements:<br>
A function expression produces a value, while a function statement performs an action. With the arrow function, it is important to remember that statements need to have curly braces. Once the curly braces are present, you always need to write return as well.

```var feedTheCat = (cat) => {
  if (cat === 'hungry') {
    return 'Feed the cat';
  } else {
    return 'Do not feed the cat';
  }
}
```

5) Block Body:<br>
If your function is in a block, you must also use the explicit return statement:
```var addValues = (x, y) => {
  return x + y
}
```

6) Object Literals:<br>
If you are returning an object literal, it needs to be wrapped in parentheses. This forces the interpreter to evaluate what is inside the parentheses, and the object literal is returned.
```x =>({ y: x })```

7) Anonymous:<br>

This anonymity creates some issues:
1) Harder to debug

When you get an error, you will not be able to trace the name of the function or the exact line number where it occurred.

2) No self-referencing

If your function needs to have a self-reference at any point (e.g. recursion, event handler that needs to unbind), it will not work.

### No binding of this:

In classic function expressions, the this keyword is bound to different values based on the context in which it is called. With arrow functions however, this is lexically bound. It means that it uses this from the code that contains the arrow function.

```
// ES5
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(function() {
      console.log(this.id);
    }.bind(this), 1000);
  }
};


// ES6
var obj = {
  id: 42,
  counter: function counter() {
    setTimeout(() => {
      console.log(this.id);
    }, 1000);
  }
};
```

When not to use them:
1. Object Methods 
When you call cat.jumps, the number of lives does not decrease. It is because this is not bound to anything, and will inherit the value of this from its parent scope.
```
var cat = {
  lives: 9,
  jumps: () => {
    this.lives--;
  }
}
```

2. Callback with dynamic context 
```var button = document.getElementById('press');
button.addEventListener('click', () => {
  this.classList.toggle('on');
});
```
If we click the button, we would get a TypeError. It is because this is not bound to the button, but instead bound to its parent scope.

3. Less readable Code

When you should use them

Arrow functions shine best with anything that requires this to be bound to the context, and not the function itself.

Despite the fact that they are anonymous, I also like using them with methods such as map and reduce, because I think it makes my code more readable. To me, the pros outweigh the cons.

Some of the differences & Limitations are:
1. Does not have its own bindings to this or super, and should not be used as methods.
2. Does not have new.target keyword.
3. Not suitable for call, apply and bind methods, which generally rely on establishing a scope.
4. Can not be used as constructors.
5. Can not use yield, within its body.

### The Arrow Function Breakdown:

```
function (a){
  return a + 100;
}

// Arrow Function Break Down

// 1. Remove the word "function" and place arrow between the argument and opening body bracket
(a) => {
  return a + 100;
}

// 2. Remove the body braces and word "return" -- the return is implied.
(a) => a + 100;

// 3. Remove the argument parentheses
a => a + 100;
```
```
// Traditional Function
function bob (a){
  return a + 100;
}

// Arrow Function
let bob = a => a + 100;
```

#### The handling of this is also different in arrow functions:

In short, with arrow functions there are no binding of this.
In regular functions the this keyword represented the object that called the function, which could be the window, the document, a button or whatever.
With arrow functions the this keyword always represents the object that defined the arrow function.

With a regular function this represents the object that calls the function:

```
Click the button to execute the "hello" function again, and you will see that this time "this" represents the button object.
[object Window][object HTMLButtonElement]
```

With an arrow function this represents the owner of the function:
```
Click the button to execute the "hello" function again, and you will see that "this" still represents the window object.
[object Window][object Window]
```

Remember these differences when you are working with functions. Sometimes the behavior of regular functions is what you want, if not, use arrow functions.

## JavaScript Object Destructuring:

[Article Link](https://blog.greenroots.info/javascript-object-destructuring-usages-you-must-know)

We use JavaScript objects to store data and retrieve it later. We store data(aka information) in key-value pairs. The key-value pair is also known as the object properties. 

```
const employee = {
  id: 007,
  name: 'James',
  dept: 'Spy'
}
```
Their is mechanism to hand the properties of objects in much more innovative ways. This mechanism is called Destructuring.

### Using destructuring to retrieve values from an object

```
//Early Days
const id = employee.id;
const name = employee.name;
```
No doubt it works perfectly. But think about the tiring typing(or copy-paste-edit) work when you have to do it for many property values? 

```const { id, name } = employee;```

Here, we use the object's key names to create variables and assign them with the value from the object for the same key. Here, we use the object's key names to create variables and assign them with the value from the object for the same key.

### Use destructuring to retrieve values from a nested object

The object's key can have another object as a value and form a nested object.

```
const employee = {
  id: 007,
  name: 'James',
  dept: {
    id: 'D001',
    name: 'Spy',
    address: {
      street: '30 Wellington Square',
      city: 'Chelsea'  
    }
  }  
}
```

```
// Traditional Way
const street = employee.dept.address.street;
```

```
//Modern Ways
const { dept: { address: { street } } } = employee;
console.log(street);
```

### Define a new variable with object destructuring

There could be a situation where you are unsure if the object has a specific key while retrieving its value. Also, you may want to create a new variable with a default value in case the key is unavailable in the object.

Let's take this employee object for an example,
```
const employee = {
  id: 007,
  name: 'James',
  dept: 'Spy'
}
```
Assume we are trying to retrieve the value of the age property, which is not present in the object. A traditional way to do that is,

Traditional Way
```const age = employee.age ? employee.age : 25;```

Modern Way
```const { name, age=25 } = employee;
console.log(age);
```

### Bit of Magic
``` 
const {name, dept, message = `${name} is ${dept}`} = employee;
console.log(message);
```
Here, we have created a new varaiable message and then assign it with avaialble value of name and dept. Pretty good.

### Using JavaScript object destructuring aliases

In JavaScript object destructuring, you can give your destructured variables an alias name. It comes in very handy to reduce the chances of variable name conflicts.

```
const employee = {
  id: 007,
  name: 'James',
  dept: 'Spy'
}
```

Let's assume your source code has an existing variable named dept. So if we use the same variable name in destructuring, there will be a name conflict.
Instead, you can use an alias name to create the variable with this new name. For example, we can use the alias name department in this case. 

```
const { dept: department } = employee;
console.log(department); //Spy
```

### Handling dynamic name property with object destructuring
These objects may contain dynamic data such that, as a client, we may not even know the property key names in advance.

```
// Example
const employee = {
  id: 007,
  name: 'James',
  dept: 'Spy'
}
```

Can we write a function that returns the value of the employee object properties when we pass a key as an argument? Yeah, so it means we will not hard-code the key name inside the function. It is dynamic for the function.

Here is the code snippet to showcase how we may call the function.

```
// Traditional Way
const id = getPropertyValue('id');
const name = getPropertyValue('name');

console.log(id, name); // 7 'James'
```

Defining the Function 

```function getPropertyValue(key) {
    const { [key]: returnValue } = employee;   
    return returnValue;
}
```

### Destructure objects in the function argument and return value

You can use object destructuring to pass the property values as arguments to the function.

```
const employee = {
  id: 007,
  name: 'James',
  dept: 'Spy'
}
```

```
function logEmployee({name, dept}) {
  console.log(`${name} is ${dept}`); 
}
```

Just realize how simple it is. You don't need to take the entire object as an argument and pick the required property values. You pass the values directly as function arguments and use them inside.

logEmployee(employee); // James is Spy

**Note:**
If a function returns an _object_, you can destructure the values directly into variables.

```
function getUser() {
  return {
    'name': 'Alex',
    'age': 45
  }
}
```

```
const { age } = getUser();
console.log(age); // 45
```

### Use object destructuring in loops

Let's think of an array of employee objects. We want to iterate through the array and want to use the property values of each of the employee object.

```
const employees= [
  { 
      'name': 'Alex',
      'address': '15th Park Avenue',
      'age': 43
  },
  { 
      'name': 'John',
      'address': 'USA',
      'age': 33
  },
  { 
      'name': 'Ravi',
      'address': 'Bangalore',
      'age': 16
  }
];
```

You can use the for-of loop to loop through the employees object and then use the object destructuring assignment syntax to retrieve the details.

```
for(let {name, age} of employees) {
  console.log(`${name} is ${age} years old!!!`);
}
```

## JavaScript Synchronous vs Asynchronous - Call Stack, Promises & More

[Article Link](https://www.freecodecamp.org/news/synchronous-vs-asynchronous-in-javascript/)<br>

JavaScript is a single-threaded, non-blocking, asynchronous, concurrent programming language with lots of flexibility.

If you understand what single-threaded means, you'll likely mostly associate it with synchronous operations. How can JavaScript be asynchronous, then?

### JavaScript Functions:
In JavaScript, you can create and modify a function, use it as an argument, return it from another function, and assign it to a variable. All these abilities allow us to use functions everywhere to place a bunch of code logically.
```
// Define a function
function f1() {
    // Do something
    // Do something again
    // Again
    // So on...
}

// Invoke the function
f1();
```
By default, every line in a function executes sequentially, one line at a time. The same is applicable even when you invoke multiple functions in your code. Again, line by line.

### Synchronous JavaScript:
So what happens when a function is defined and invoke it. The JS engine maintains a stack data structure called function execution stack. The purpose of the stack is to track the current function in execution. 

#### Inside a function execution stack **(Call Stack)** :<br>
1. When the JavaScript engine invokes a function, it adds it to the stack, and the execution starts.
2. If the currently executed function calls another function, the engine adds the second function to the stack and starts executing it.
3. Once it finishes executing the second function, the engine takes it out from the stack.
4. The control goes back to resume the execution of the first function from the point it left it last time.
5. Once the execution of the first function is over, the engine takes it out of the stack.
6. Continue the same way until there is nothing to put into the stack.

A quick example of the flow for the execution order:

```
function f1() {
  // some code
}
function f2() {
  // some code
}
function f3() {
  // some code
}

// Invoke the functions one by one
f1();
f2();
f3();
```

First, f1() goes into the stack, executes, and pops out. Then f2() does the same, and finally f3(). After that, the stack is empty, with nothing else to execute.

A complex example:

```
function f1() {
  // Some code
}
function f2() {
  f1();
}
function f3() {
  f2();
}
f3();
```

Notice that first f3() gets into the stack, invoking another function, f2(). So now f2() gets inside while f3() remains in the stack. The f2() function invokes f1(). So, time for f1() to go inside the stack with both f2() and f3() remaining inside.<br>
First, f1() finishes executing and comes out of the stack. Right after that f2() finishes, and finally f3().
This is the Synchronous part of JavaScript. 

### Asynchronous JavaScript – How Browser APIs and Promises Work

The word asynchronous means not occurring at the same time. Typically, executing things in sequence works well. But you may sometimes need to fetch data from the server or execute a function with a delay, something you do not anticipate occurring NOW. So, you want the code to execute asynchronously.

In this circumstance, you may not want the JS engine to halt the execution of the other sequential code. So, the JavaScript engine needs to manage things a bit more efficiently in this case.

The two triggers for asynchronous JS operations are:
1. Browser API/Web API: These include methods like setTimeout, or event handlers like click, mouse over, scroll, and many more.
2. Promises: A unique JavaScript object that allows us to perform asynchronous operations.

### Handling Browser Api/Web Api:

Browser APIs like setTimeout and event handlers rely on callback functions.

```
function printMe() {
  console.log('print me');
}

setTimeout(printMe, 2000);
```

The setTimeout function executes a function after a certain amount of time has elapsed. In the code above, the text print me logs into the console after a delay of 2 seconds.

An Example:

```
function printMe() {
  console.log('print me');
}

function test() {
  console.log('test');
}

setTimeout(printMe, 2000);
test();
```

Will the JavaScript engine wait for 2 seconds to go to the invocation of the test() function and output this:
```
printMe
test
```

OR, Will it manage to keep the callback function of setTimeout aside and continue its other executions:

```
test
printMe
```
The last one is correct as this is where the asynchronous mechanism comes.

### How the JavaScript Callback Queue Works (Task Queue)

JavaScript maintains a queue of callback functions. It is called a callback queue or task queue. A queue data structure is First-In-First-Out(FIFO). 

#### Step process how Task Queue works:
1. When a Browser API occurs, park the callback functions in a queue.
2. Keep executing code as usual in the stack.
3. The event loop checks if there is a callback function in the queue.
4. If so, pull the callback function from the queue to the stack and execute.
5. Continue the loop.

```
// Code Example

function f1() {
    console.log('f1');
}

function f2() {
    console.log('f2');
}

function main() {
    console.log('main');
    
    setTimeout(f1, 0);
    
    f2();
}

main();
```
Here, the output is 
```
main
f2
f1
```

As we may think there is no delay in setTimout which makes it to execute directly but it does not happen and it goes to event loop mechanism and continues other code.

A clear Step of how this will work:

1) The main() function gets inside the call stack.
2) It has a console log to print the word main. The console.log('main') executes and goes out of the stack.
3) The setTimeout browser API takes place.
4) The callback function puts it into the callback queue.
5) In the stack, execution occurs as usual, so f2() gets into the stack. The console log of f2() executes. Both go out of the stack.
6) The main() also pops out of the stack.
7) The event loop recognizes that the call stack is empty, and there is a callback function in the queue.
8) The callback function f1() then goes into the stack. Execution starts. The console log executes, and f1() also comes out of the stack.
9) At this point, nothing else is in the stack and queue to execute further.

### Promises




