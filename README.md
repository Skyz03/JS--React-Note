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
[Article Link](https://www.freecodecamp.org/news/when-and-why-you-should-use-es6-arrow-functions-and-when-you-shouldnt-3d851d7f0b26/)
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


