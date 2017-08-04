## Named Function Expressions
There are two ways to declare functions.
#### Anon Function Expressions
```javascript
var app = function() {
  // code here
}
```

#### Named Function Expressions

```javascript
var handler  = function handler() {
  // code here
}
```

The identifier after the `function` keyword will accessible inside of itself
only.

### What is the difference between an anonymous function expression and a named function expression?
- You should always prefer named function over anonymous functions.
  - Theree main benefits:
      - Handy function self-reference
          - This is specially useful for recursion. This is function referring to itself.
      -  More debuggable stack trace
          - super helpful specially in production
          - It uses the function name in the stack trace
  - More self-documenting code 
