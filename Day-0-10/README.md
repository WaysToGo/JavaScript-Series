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

### Functions

u know how javascript know if it is function or not?
function is also a object which has some special propery called [[Call]] by which cannot be accesed programmatically


ways to declare functions are

//first way


var result  = add(5,5);

function add(num1,num2){
    return num1+num2;
}

//second way

var result =add(5,5)

var add=function(num1,num2){
        return num1+num2;
}

what do u think output will be ?

first way works fine because ,fucnction hosting will only happens to function which value is known ahead of time
like in first way we use function syntax to create function which makes compiler to understand that that is a function and it will add(hoist) these functions  to the top .

and in the second way it throws error saying that add is not a function

as functions can be assigned to variables which makes javascript more powerfull language

consider example with sort()
sort accepts  an optional  function which can be used as comparison operator
since sort method converts every item in the array to string and then compares we can pass a function which will compare two numbers and can be used to sort numbers

var num=[9,8,5,2,10];
num.sort((a,b)=>a-b) //returns [2,4,8,9,10] in sorted order    a and b first and second numbers
// note here (a,b)=>a-b is short syntax for function(a,b){return a-b;} and this function is anonynous function

another unique aspect of js is that u can pass any number of arguments to the function and values can be accesed by using array-like structure called arguments


example

function a(){
    return arguments[0];
}

a("hi")// returns "hi"

and length of function a will be zero





