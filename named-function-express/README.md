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
  - Three main benefits:
      - Handy function self-reference
          - This is specially useful for recursion. This is function referring to itself.
      -  More debuggable stack trace
          - super helpful specially in production
          - It uses the function name in the stack trace
  - More self-documenting code

- - -
## Lexical Scope
- - -

### Lexical Scope

```javascript
function foo() {
  var bar = 'bar';
  function baz() {
    console.log(bar) // lexical scope
  }
  baz();

}
foo();
```

- No matter what, the `bar` variable that is being console logged is only referring to the one declared inside of the function; it is already set. This is called a lexical scope.

### Dynamic Scope

```javascript
// theoretical dynamic scoping
function foo(){
  console.log(bar); // dynamic = execution context
}

function baz() {
  var bar = 'bar';
  foo(); // walks up the stack to find 'bar'
}

baz();

```

## Function Scoping

```javascript
var foo = 'foo';

var foo = 'foo2';
console.log(foo); // 'foo2'

console.log(foo); // 'foo2' --oops
```

### How Do We Fix Colliding Variables ?
- We can fix this by creating a scope to contain and encapsulate

```javascript
var foo = 'foo';

function bob() {
  var foo = 'foo2';
  console.log(foo); // 'foo2'
}
bob();

console.log(foo); // 'foo' -- phew!
```

- We use function scoping to protect it from collision or access. There is however a downside to this!

- We just created `bob` which someone else might collide with, the very thing we were trying to avoid to begin with.

## IIFE Pattern
```javascript

var foo = 'foo';

(function bob() {
  var foo = 'foo2';
  console.log(foo); // 'foo2'
})();

console.log(foo); // 'foo'

```

- Now, after turning the `bob` function into an `IIFE`, we are no longer polluting the global scope because of this function expression. This pattern is called `IIFE`
