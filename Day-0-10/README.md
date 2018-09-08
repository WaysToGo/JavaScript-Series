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

note : Array.isArray(arguments) always returns false.

example

function a(){
    return arguments[0];
}

a("hi")// returns "hi"
a.length// returns 0


## Day 2 of JavaScript

### Objects


consider a person Object which has a name and sayName function

var person={
    name:"Reddy",
    sayName:function(){
        console.log(person.name);
    }
}

as u can see if u want to change the name of variable person Then  u need to change the value in sayName function this will become hard to maintain if we are writing a very  long objects

so what would be the solution for this ?

"this" is the solution  ,every object in Javascript has the this context

same person can be re written as

var person={
    name:"Reddy",
    sayName:function(){
        console.log(this.name);
    }
}// here  i am not  using arrow function since arrow function will take the scope of parent

if we can do this then we can try something else example

function sayNameForAll(){
    console.log(this.name)
}


var person1={
    name:"reddy",
    sayName=sayNameForAll
}

person1.sayName()// logs reddy

 the ability to change the value of this of functions  is the key for good object oriented programming

 so how can we change the this  value in functions?

 this can be done in three different ways they are call   apply and bind

 example for call

function sayNameForAll(value){
    console.log(value +"::"+ this.name)
}


var person1={
    name:"reddy", //because of call() method we dont need to add sayNameForAll to each object
    }

sayNameForAll.call(person1,"Hey my name is ")// Hey my name is reddy

so what does call do?
call will set the value of this explicitly instad of letting Javascript engine  do it automatically

example for apply

apply is similar to call the only difference is that it takes the iist of arguments


function sayNameForAll(value){
    console.log(value +"::"+ this.name)
}


var person1={
    name:"reddy",
    }

sayNameForAll.apply(person1,["Hey my name is "])// output Hey my name is ::reddy


bind this will behave diffently than other two(call,apply)

function sayNameForAll(value){
    console.log(value +"::"+ this.name)
}


var person1={
    name:"reddy",
    }

var sayNameforPerson1=sayNameForAll.bind(person1);

sayNameforPerson1("Hey my name is ")//output Hey my name is ::reddy

var sayNameforPerson1WithArgument=sayNameForAll.bind(person1,["Hey my name is "])// this will also bind the value of first argument

sayNameforPerson1WithArgument()//output Hey my name is ::reddy
// even if we call sayNameforPerson1WithArgument with argument the out put will not change

once bind is done  this  value wont change


#### Objects Deep dive

As we know that we can add and remove values in object any time .Here i am going to explain how it works internally

Internally Object has method which are used to set the value of Object they are

[[Put]],[[Set]],[[Delete]]

when we are setting the value of property to the object for the first time then [[Put]] is called


Example

var person={
    name:"reddy" // here [[Put]] comes to play to set the values
}
person.name="other" // here [[Set]] will update the value of person name to other

console.log(person.name)// Output:other

delete person.name
console.log(person.name)//Output:undefined


[[Put]] method will create he spot for  object to store the property ,this will create won property called name in perosn object

[[Set]] Set is called if that propery already exists and it will update the value of name from "reddy" to "other"

[[Delete]] delete will delete property in the object as u can see in the above example after delete the value is undefinded


Enumerable

By default all the property in object are enumerable which means [[Enumerable]] value is set to true

ways to iterate are

for...in //use key value pair to oterate
Object.keys() //will return the array of keys which can be used to iterate


is there any difference between these two ways?

yes,for...in will also iterate the prototype properties also
while Object.keys()  will only the list of keys which are own properties of object

not all properties are enumerable,most of native methods are not enumerable

Then how to test if they are enumerable?

var person1 = {
 name: "Reddy"
};

console.log(person1.propertyIsEnumerable("name"));// Output true

## Day 3 of JavaScript


There are two different types of properties they are Data properties and Accessor properties

Data properites are the values like name from earlier examples

and Accessor properties are getter and setter methods which are used to access these values

```javascript
example
var person={
    _name:"Reddy",//_name is naming convention to tell that it is priveate but in real it is not


    get name (){             //get is a special key word
        return this._name;
    },
    set name(val){
        this._name=val;
    }
}

console.log(person.name)// Reddy


```

in the above example we can create only getter to get the value and only setter to change the value

as we discussed earlier about enumberable we can set thee value ehile defining property using

Object.defineProperty()

example

```javascript

var person={
    name:"Reddy"
    }
Object.defineProperty(person,"name",{enumerable:false});
console.log(person.propertyIsEnumerable("name")); //returns false

Object.defineProperty(person, "name", {
 configurable: false // makes object property nonenumerable and nonconfigurable meaining u cannot delete and change the value

});


Object.defineProperty(person1, "name", {
 configurable: true// once it is set to flase we cannot change it again to true
});


```
Data property

data property will have two additonal attributes [[Value]] and [[Writable]]

[[Value]] holds the value of property and [[Writable]] is by default true and can be chaged using defineProperty

```javascript

var person = {};

Object.defineProperty(person, "name", {
 value: "Reddy",
 enumerable: true,
 configurable: true,
 writable: true
});


Object.defineProperty(person, "name", {
 value: "Reddy"
});// if we define in this way the value of enumerable, configurable,writable becomes false

// so the value cannot be changed

```
to get the property values


```javascript
var person = {
 name: "Reddy"
};
var descriptor = Object.getOwnPropertyDescriptor(person, "name");
console.log(descriptor.enumerable); // true
console.log(descriptor.configurable); // true
console.log(descriptor.writable); // true
console.log(descriptor.value); //"Reddy"
```

Preventing Object modification

there are different ways to do this

var person = {
 name: "Reddy"
};


1) Object.preventExtensions(person)// cannot add any property after this

2) Object.seal(person)// cannot add and remove any property configurable will become false
3) Object.freeze() // it is sealed and writable also set to false means u cannot even edit the property





## Day 4 of JavaScript

### Prototypes


To appriciate the usage of prototype we need to know about the constructors

Constructor is simply a function which is used with new to create a Object

The only difference is that name should start with capital letter

example
function Person(){

}

var Person1=new Person()//
or
var Person1=new Person//can be written in this way if we are not passing any arguments

Person1 instanceOf Person //returns true

```javascript
function Person(name) {
 this.name = name;
 this.sayName = function() {
 console.log(this.name);
 };
}

var Person1 = new Person;//person1 also has the sayName consider if we have 100 insances we have 100 sayName functions copied to each instance

var Person2 = new Person;//same sayName is copied here also





```

so how to solve this?

here comes our savior prototype

```javascript

function Person(name) {
 this.name = name;
}
 Person.prototype.sayName = function() {
 console.log(this.name);
};
var person1 = new Person("Reddy");
var person2 = new Person("Shiva");
console.log(person1.name); // "Reddy"
console.log(person2.name); // "Shiva"
person1.sayName(); // outputs "Reddy"
person2.sayName(); //outputs "Shiva"

```

here the sayName function is added to  Person prototype and when a new instance is created that will be refered

Prototype is the shared memory between instances,like a static method in programming languages like Java


even if we freeze the the Object we can still add the properties to prototype from which the instance is created

```javascript
var person1 = new Person("Reddy");

Object.freeze(person1);
Person.prototype.sayHi = function() {
 console.log("Hi");
};
person1.sayHi(); // outputs "Hi"

```



## Day 5 of JavaScript

 ###inheritance

 list of methods inherited from object are
```javascript

hasOwnProperty()// Determines whether an own property with the given name exists

propertyIsEnumerable()// Determines whether an own property is enumerable

isPrototypeOf() //Determines whether the object is the prototype of another

valueOf() //Returns the value representation of the object

toString() //Returns a string representation of the object
```


## Day 6 of JavaScript


valueOf()

The valueOf() method gets called whenever an operator is used on an
object. By default, valueOf() simply returns the object instance. The
primitive wrapper types override valueOf() so that it returns a string for
String, a Boolean for Boolean, and a number for Number


toString()

The toString() method is called as a fallback whenever valueOf() returns a
reference value instead of a primitive value. It is also implicitly called on
primitive values whenever JavaScript is expecting a string. For example,
when a string is used as one operand for the plus operator, the other
operand is automatically converted to a string. If the other operand is a
primitive value, it is converted into a string representation (for example,
true becomes "true"), but if it is a reference value, then valueOf() is called.
If valueOf() returns a reference value, toString() is called and the returned
value is used

Effective JavaScript 68 Specific Ways to Harness the Power of JavaScript (Effective Software Development Series)

daily goal- cover daily 10 ways

rules of using semicolon

- if it  statment start with (, [, +, -, or /  javascript wont add semicolon by default
- after return ,break,postfix,prefix ,throw  javascript will add semicolon by default
- for for loop head also it wont add semicolons

## Day 7 of JavaScript

day-7
closure
variable hoisting
variable scope
iffy


## Day 8 of JavaScript

Change of track for few days

Angular
 @injectable
 what happens if we give injectable
 even if we dont add also it will works if no dependencys are available

 if it is a simple class then no Problem
 if that class needs http or some other things the generated javascript code wont have enough information
 if we add injectable to then compiled javascript code has enough information of what to import to make it work

Routes
    export const appRoutes:Routes // this will give intellisence for router
    canActive -> is used if page is not available and to redirect user to 404 or some page then it can be used
    canDeactive -> is used Deactive all routes (can be used when user enters data and dont save the data and try to move to another page )
    some times page loads partially loads and when the data comes the rest of the page is loaded this can be annoying ,can be solved by using preloading (setting the data to the route as parameter and once data comes the page loads automatically ) at once

Active route
some times when we want to show the user on which page he is in so we add routerLinkActive=active
after adding this also the other router are also active the starting of page is same example
/foo/ ->this is as active when foo route is taken
/foo/bar  ->this and /foo also actived since both starts with foo to solve this use  routerLinkActiveOptons="{exact:true}"

lazy Loading
Having a different module files can be helpful to lazy load pages when  required

Things to be noted while creating the modules
it uses the CommonModule  instad of BrowserModule
for RouterModule we use forChild() instad of forRoot()
and in main route file add loadChildren to lazy load children when required

for better viewing use barrels (import and export all files from one file and use that file to import which will make it look proper)

## Day 9 of JavaScript

## Day 10 of JavaScript
