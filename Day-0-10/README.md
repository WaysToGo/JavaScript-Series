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
console.log(a instanceof Array )// this will return true this also get tricky because every thing is eventually points to Object so it will return true
console.log(a instanceof Object  )// returns true

so what is the best way to find?
Array.isArray(a)//hey this will return true finally we got some solution but this is not supported in Ie 8 (who cares about ie 8 :joy: )

primitive wrapper types
The things(references ) that are created by default
example
var a="some Text"
var char=a.charAt(0)//first line we set it as primitive and in second line it is behaving like an object with references like charAt() etc

so how does it works ?

var a="some Text"//when we set the value the followings thigs are done by browser

var temp=new String(a)
var char=temp.charAt(0); //this process is known as auto boxing
temp=null //garbage collection

so it is behaving like an object so can i set values :confused: ?

as we can see in above example the temp is set to null as soon as we use carAt() so even if we set the value the value will be null :joy:


## Day 1 of Javascript