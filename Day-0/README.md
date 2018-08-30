## Day 0 of Javascript

### Introduction

### Object oriented Javascript the beginning of the journy

primitive and referene types

In other languages the generally Object Oriented the primitive data types are stored in stack and references are stored in heap
Primitive types
- Boolean
- Number
- String
- Null
- Undefinded

There are diffetent ways to create object in javascript and literal method is recommended
example
 var obj =new Object()// is one way of creating object
 var obj={} // this is another way of creating object

 second way is much readable and easy to write which are called lterals
 and more over if the functions are created using new (constructor form) it is harder to test as debugger cannot recognize these type of functions therefore it will act as the black box in the application


other than functon type of the object will return object so it is better to use instanceof  to check correctly
example
var a=[]
typeof a//returns object
//else we can write
console.log(a instanceof Array )// this will return true     this also get tricky because every thing is eventually points to Object so it will return true even for

console.log(a instanceof Object  )// returns true