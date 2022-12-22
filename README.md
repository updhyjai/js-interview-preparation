# js-interview-preparation

1. How to make javascript multi-threaded?
2. How are .call and arrow-functions are related to each other?
3. What is the use of closures?
4. Difference between setImmediate and nextTick()?
5. How to implement shouldComponentUpdate() in functional component?
6. What is dunder proto in JS?
7. Difference between for-of and for-in loop?
8. What is DOM?
9. What is the difference between Redux-thunk and Redux-saga?
10. How does multiple asynchronous request handled by the JS?


<details><summary>11. How to detect and handle if JS is supported in client browser?</summary>
<p>
#### We can achieve this by using ```<noscript></noscript>``` tag. For example:

```html
<html>
  <head>
    <title>Demo of Checking if JavaScript is enabled in web browser</title>
  </head>
  <body>
    <noscript>
      <meta http-equiv="refresh" content="5; URL=https://www.google.com" />

      Are you using a browser that doesn't support JavaScript?<br /><br />

      If your browser does not support JavaScript, you can upgrade to a newer
      browser<br /><br />

      If you have disabled JavaScript, you must re-enable JavaScript to use this
      page. To enable JavaScript:
    </noscript>

    <br /><br />

    If you are not seeing any message above this line then you have JavaScript
    enabled in your browser.
  </body>
</html>
```

</p>
</details>
