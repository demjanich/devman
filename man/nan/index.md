The isNaN() function returns true if the value is NaN (Not-a-Number), and false if not.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN

```
let isNaN = function(value) {
    let n = Number(value);
    return n !== n;
};
```

The Number.isNaN() method determines whether the passed value is ```NaN``` and its type is ```Number```. It is a more robust version of the original, global ```isNaN()```.

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN

https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/isNaN#Confusing_special-case_behavior


```
<p id="demo"></p>

<script>

  let res = "";
  let x = 5;
  let y = 'test';
  
  res = res + Number('Hello') + ": Number('test')<br>";
  res = res + Number.isNaN('Hello') + ": Number.isNaN('Hello')<br>";
  res = res + isNaN('Hello') + ": 'Hello'<br>";
  
  
  // false
  res = res + (x !== x) + ": NaN == NaN<br>";
  res = res + (y !== y) + ": NaN == NaN<br>";
  
  res = res + (NaN == NaN) + ": NaN == NaN<br>";
  res = res + (NaN == 'test') + ": NaN == 'test'<br>";
  res = res + isNaN(123) + ": 123<br>";
  res = res + isNaN(-1.23) + ": -1.23<br>";
  res = res + isNaN(5-2) + ": 5-2<br>";
  res = res + isNaN(0) + ": 0<br>";
  res = res + isNaN('') + ": ''<br>";
  res = res + isNaN(true) + ": true<br>";  
  res = res + isNaN(false) + ": false<br>";  
  res = res + isNaN('123') + ": '123'<br>";  
  res = res + isNaN("") + ": \"\"<br>";
  res = res + isNaN(null) + ": null<br>";
  
  res = res + "<br>";
  
  
  // true 
  res = res + isNaN('Hello') + ": 'Hello'<br>";
  res = res + isNaN('2005/12/12') + ": '2005/12/12'<br>";
  res = res + isNaN(undefined) + ": undefined<br>";
  res = res + isNaN('NaN') + ": 'NaN'<br>";
  res = res + isNaN(NaN) + ": NaN<br>";
  res = res + isNaN(0 / 0) + ": 0 / 0<br>";  
  res = res + isNaN({}) + ": {}<br>";
  res = res + isNaN(".") + ": \".\"<br>";  

  document.getElementById("demo").innerHTML = res;

</script>
```

```
NaN: Number('test')
false: 'Hello'
true: 'Hello'
false: NaN == NaN
false: NaN == NaN
false: NaN == NaN
false: NaN == 'test'
false: 123
false: -1.23
false: 5-2
false: 0
false: ''
false: true
false: false
false: '123'
false: ""
false: null

true: 'Hello'
true: '2005/12/12'
true: undefined
true: 'NaN'
true: NaN
true: 0 / 0
true: {}
true: "."
```
