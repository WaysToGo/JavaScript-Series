## Day 11 of JavaScript

Getting started with Angular

patterns in javascript

classic pattern
``` javascript
var sample = (function() {
    var a = 10;
    var b = 20;
    var getSum = function() {
        return a + b
    }
    return {
        sum: getSum
    }
})();

sample.sum()// returns 30
```

CommonJs pattern

```javascript
var sample = function() {
    var a = 10;
    var b = 20;
    this.sum = function() {
        return a + b
    }
}; // usually this funtion is exported and used in another function
var test = new sample;
test.sum()// returns 30

```


## Day 12 of JavaScript

## Day 13 of JavaScript

## Day 14 of JavaScript

## Day 15 of JavaScript

## Day 16 of JavaScript

## Day 17 of JavaScript

## Day 18 of JavaScript

## Day 19 of JavaScript

## Day 20 of JavaScript
