# JS--React-Note

## The story behind Let, Const & Var
[Link](https://www.freecodecamp.org/news/understanding-let-const-and-var-keywords/)

Understanding var, let, and const in ```Scope, Reassigning and Accessing the variables```

### Scope:
In JavaScript, we use scope as a way to identify where and whether we can use the respective declared variable. The variables may exist within a block, inside a function, or outside a function and block.

Their are 3 types of Scope:
1) Block:
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

2) Functional:


3) Global
