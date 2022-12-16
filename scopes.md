1. 
    
  ```javascript
  var foo = 'bar';

  function bar(){
    var foo = 'baz';

    function baz(foo){
      foo = 'bam';
      bam = 'yay'
    }

    baz()
  }

  bar();
  console.log(foo);
  console.log(bam);
  console.log(baz());
```
  <details><summary>Solution</summary>
  <p>
    
```
bar
yay

console.log(baz());
        ^
ReferenceError: baz is not defined
```
  </p>
</details>


2.

```javascript
var foo = function bar(){
  var foo = 'baz';
  
  function baz(foo){
    foo = bar;
    console.log(foo);
  }
  baz()
}

foo()
bar()
```
 <details><summary>Solution</summary>
  <p>
    
```
[Function: bar]

bar()
^

ReferenceError: bar is not defined
```
  </p>
</details>

3.

```javascript
var bar = 'yay'

function foo(str){
  eval(str)
  console.log(bar)
}

foo('var bar =42')
```
 <details><summary>Solution</summary>
  <p>
    
```
42
```
  </p>
</details>

4.

```javascript
var bar = 'yay'

function foo(str){
  eval(str)
  console.log(bar)
}

foo()
```
 <details><summary>Solution</summary>
  <p>
    
```
yay
```
  </p>
</details>

5.

```javascript
var obj = {
  a: 2,
  b: 3,
  c: 4
}

obj.a = obj.b + obj.c;
obj.c = obj.b - obj.a;

with(obj){
  a = b + c;  // equivalent obj.a = obj.b + obj.c;
  c = b - a;  // equivalent obj.c = obj.b - obj.a;
  d = 3;
}

console.log(obj.d)
console.log(d)
```
 <details><summary>Solution</summary>
  <p>
    
```
undefined
3
```
  </p>
</details>

6.

```javascript
var foo = 'bar';

(function(){
  var foo = 42;
  console.log(foo);
})()

console.log(foo)
```
 <details><summary>Solution</summary>
  <p>
    
```
42
bar
```
  </p>
</details>

7.

```javascript
var foo = 'bar';

(function(bar){
  var foo = bar;
  console.log(foo);
})(foo)

console.log(foo)
```
 <details><summary>Solution</summary>
  <p>
    
```
bar
bar
```
  </p>

</details>

8.

```javascript
(function iffe(){
    var foo = 'bye';
    console.log(foo)
}())
```
 <details><summary>Solution</summary>
  <p>
    
```
bye
```
  </p>
</details>

## Hoisting

8.

```javascript
console.log(a)
console.log(b)
var a = b;
var b = 2;
console.log(b)
console.log(a)
```
<details>
    <summary>Solution</summary>
       
    undefined
    undefined
    2
    undefined


</details>

9.

```javascript
var a = b();
var c = 10;
console.log(a);

var e = d();
var f = 20;
console.log(e)

function b(){
  return c;
}

var d = function(){
  return f;
}
```
<details>
    <summary>Solution</summary>
       
    undefined

    var e = d();
        ^
    TypeError: d is not a function
    
> Reason: Function declaration gets hoisted to the top while function expression does not. So declaration of variable 'd' gets hoisted but its assignment is still pending until the line gets executed, same goes for variable 'c' whose declaration goes to the top but the value is assigned after the execution of the 'function b'. Think of it like below:
    
    
```javascript
function b(){
    return c;
} 
var a;
var c;
var e;
var f;
var d;

a = b();
c = 10;
console.log(a);

e = d();
f = 20;
console.log(e)

d = function(){
  return f;
}
```
    
</details>


10.

```javascript
var c = 10;
var a = b();
console.log(a);

var e = d();
var f = 20;
console.log(e)

function b(){
  return c;
}

function d(){
  return f;
}
```
<details>
    <summary>Solution</summary>
       
    10
    undefined

</details>

11.

```javascript
fn();
f();
var fn = 2;
var f = 3;
function fn(){
  console.log('Hi');
}


function fn(){
  console.log('Bye');
}
```
<details>
    <summary>Solution</summary>
       
    Bye

    f();
    ^
    TypeError: f is not a function
    
> Reason: Functions get hoisted before variables and all other functions are overwritten with the most recent one encountered and variables declared with the same name as function get ignored. Think of it like below:
    
    
```javascript
function fn(){
  console.log('Hi');
}


function fn(){
  console.log('Bye');
}

var fn; //ignored as function is already hoisted with same name and overwritten with the last (recent) one
var f;

fn();
fn = 2;
f();
f = 3;
```
    
</details>

12.

```javascript
console.log(a(1));

function a(val){
  if(val > 30) return val;
  return b(val + 2);
}

function b(val){
  return c(val) + 2;
}

function c(val){
  return a(val*2)
}
```
<details>
    <summary>Solution</summary>
       
    42
    
> Note: One of the reason Javascript does hoisting. Above is an example of Mutual Recursion where one function is depending on other and vice-versa. 
    
</details>

12.

```javascript
function fn(val){
  if(val){
    console.log(res);
    let res = val;
  }
}

fn('hi')

```
<details>
    <summary>Solution</summary>
       
    console.log(res);
                ^
    ReferenceError: Cannot access 'res' before initialization
 
    
> Reason: Temporal dead zone.
    
</details>

## this binding

13.

```javascript
function foo(){
  console.log(this.bar);
}
var bar = 'bar1';
var obj2 = {bar : 'bar2', foo : foo}
var obj3 = {bar : 'bar3', foo : obj2.foo}


foo();
obj2.foo();
obj3.foo();

```
<details>
    <summary>Solution</summary>
       
    bar1
    bar2
    bar3
    
> Reason: default binding in the case of 'foo()' which will result this to be either global or undefined (in case of strict mode) and implicit binding in case of rest.
    
</details>

14.

```javascript
var obj1 = {
  bar : 'bar1',
  foo : function(){
    console.log(this.bar);
  }
}

var obj2 = {bar: 'bar2', foo : obj1.foo};

var foo = obj1.foo;

var bar = 'bar3'

obj1.foo()
obj2.foo()
foo()

```
<details>
    <summary>Solution</summary>
       
    bar1
    bar2
    bar3
    
    
</details>

15.

```javascript
function foo(){
  var bar = 'bar1';
  baz();
}

function baz(){
  console.log(this.bar);
}

var bar = 'bar2';

foo()

```
<details>
    <summary>Solution</summary>
       
    bar2
    
</details>

16.

```javascript
function foo(){
  var bar = 'bar1';
  this.baz = baz;
  this.baz();
}

function baz(){
  console.log(this.bar);
}

var bar = 'bar2';

foo()

```
<details>
    <summary>Solution</summary>
       
    bar2
    
</details>





