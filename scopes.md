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




