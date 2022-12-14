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
