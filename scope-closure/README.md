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

Compiler : Hey global scope manager



```JavaScript
// line 1 :  formal variable declaration
var foo = 'bar';

// line 3: formal function declaration
function bar() {
  var foo = 'baz';
}


// line 7
function baz(foo) {
  foo = 'bam';
  bam = 'yay';
}
```
- - -
