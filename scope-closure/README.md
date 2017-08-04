# Topics:
- [x]  Nested
- [x] Hoisting
- [x] Closure
- [x] Modules

- - -

### Scope
- - -

- Scope has the meaning of where to look for things

#### Introduction
  - JavaScript is a compiled language and not interpreted language.

    (-) proof

    say you have a JavaScript error on line 10 in your code. How does JavaScript know about line 10 without first running line 1?

    answer:

    JavaScript already knew that there was going to be a syntax error in line 10 before running line 1 because JavaScript engine compiled it. Hence, the compilation validated the syntax long before it was handed to the engine.

    When does the lexical scope gets setup?

    answer:

    It happens during the first pass and not the second.

    JavaScript has function scope only*
- - -
\scope\

Anthropomorphic javascript conversation: compiler vs scope manager

Compiler : Hey global Scope Manager, I found a formal declaration for `foo` on `line 1`, have you ever heard of him?

Scope manager : no, never heard of him, but now that you mentioned it, let me put it in the scope bucket.

Compiler : Hey global Scope Manager, I've got an identifier called `bar` on `line 3`, have you ever heard of it?

Scope manager : no, never heard of him, but now that you mentioned it, let me put it in the scope bucket.


Shadowing :
  -  Having to variables with the same name in different scope.


```JavaScript
// line 1 :  formal variable declaration
1 var foo = 'bar';

// line 3: formal function declaration
3 function bar() {
4  var foo = 'baz';
}


// line 7
7 function baz(foo) {
8  foo = 'bam';
9  bam = 'yay';
}

```
- - -

### Execution of Function Code

Meta information : to execute the code we need more information. There is some meta information that we discover along the way. There is something very important about where a variable shows up. Because where it shows up and the context which it is used determines how it is going to behave at run-time.

LHS look-up is done when a variable appears on the left-hand side of an assignment operation, and an RHS look-up is done when a variable appears on the right-hand side of an assignment operation.

- LHS lookup is a container lookup
- RHS lookup is a value lookup

These terms stand for "Left-hand Side" and "Right-hand Side"

```JavaScript
var foo = 'bar';
```

JavaScript Virtual Machine (JVM) : Hey Global Scope Manager, I've got a LHS reference for a variable named `foo`, have you ever heard of him?  

Scope Manager : Yes, I have it (it was added in the compile time).

```JavaScript
function bar() {
  var foo = 'baz';
}
```

JavaScript Virtual Machine (JVM) : Hey Scope Manager `bar`, I've got a LHS reference for a variable named `foo`, have you ever heard of him?  

`bar` Scope Manager : Yes, I have it (it was added in the compile time).


```JavaScript
 function baz(foo) {
  foo = 'bam';
  bam = 'yay';
}
```

JavaScript Virtual Machine (JVM) : Hey Scope Manager `baz`, I've got a LHS reference for a variable named `foo`, have you ever heard of him?  

`bar` Scope Manager : Yes, I have it (it was added in the compile time).

JavaScript Virtual Machine (JVM) : Hey Scope Manager `baz`, I've got a LHS reference for a variable named `bam`, have you ever heard of him?  

`bar` Scope Manager : go fish (go up one level of scope and ask the question again)

. . .


JavaScript Virtual Machine (JVM) : Hey Global Scope Manager, I've got a LHS reference for a variable named `bam`, have you ever heard of him?  

Global Scope Manager : no, but I went ahead and created one for you anyway!

What? It created a global at run-time because it could not find one formally declared.

- If we did this in strict mode, the global scope would be prevented from creating it. It would throw a reference error, 'bam is not defined'.

- - -
### Strict Mode
- always use `strict mode`
- - -


### Example



```javascript
var foo = 'bar';

function bar() {
  var foo = 'baz';

  function baz(foo) {
    foo = 'bam';
    bam = 'yay';
  }

  baz();
}

bar();
foo; // bar
bam; // yay
baz(); // ReferenceError: Can't find variable: baz
```

## Conclusion
- - -

```javascript
var foo = function bar() {
  bar foo  = 'baz';
  function baz(foo) {
    foo = bar;
    foo;
  }
  baz();
};
foo();
bar(); // error
```

- - -

For function expression, the `bar` identifier will not be added to the enclosing scope, that's why it will generate a `reference error` when called. In other words, there is no `bar` identifier in the global scope even though it does exist. Interestingly, we do have access to `bar` inside of itself.


### Another example

```javascript
var foo;

try {
  foo.length;
}
catch(error) {
  console.log(err); // TypeError
}

console.log(err); // ReferenceError
```
