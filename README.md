# -JavaScript-Concepts

## 3.11 scope chain


    function saymyname(){
    var a='a';
    return function findname(){
        var b='b';
          console.log(b);
        return function printname(){
            var c='c';
            return 'life';
        }
    }
    }
    saymyname()()();

result -> b and life;
find name function is written in saymyname function.here find name function lexical environment is printname function.print name function lexical environment is findname function .so here's the scope work.but we can't find a result of c variable if we (console.log(c)) at 9 number line. 

### 3.13 weird js
    fun any()
    {
    height=50;
    return height
    }
  
 result->50;
 var ,let,const tell js variable environment this is a variable .but here height=50 go to global scope chain , 'use strict' can help this for not doing this kind of weird js.use it global.
 
 
    var heyhey=function doodle(){
      doodle()
      return 'something
    }
    heyhey();
can't call doodle in global , js is weird.doodle function is close in it's own function.so we can't call it from line number 37.


#### 3.14 function scope vs block scope
    if(5>4)
    {
    var x=1234;
    }
    cosole.log(x);


result->1234;
var variable can be access any line but if we use let or const linr=e number 44 we can't access them.

##### 3.17 IIFE

    var script1=(function(){
    function a(){
        return 5;
    }
    return{
        a: a
    }

    })();
    console.log(script1.a());
 result->5;
    
    
### 3.18 this keyword

2 benifits ->
1.gives methods acess to their object

    const obj={
    name: 'billy',
    sing(){
        return 'lala'+this.name;
    },
    singagain (){
       return this.sing+"!"
    }

    }
    obj.singagain()
    
    
 2.execute same code for multiple object
    
    function importantperson(){
    console.log(this.name);
    }
    const name='do'

    const obj1={
        name:'cassy',
        callname:importantperson
    }
    const obj2={
        name:'passy',
        callname:importantperson

    }
    console.log(obj1.callname())
    
  result->cassy
  
  ### 3.20 call, apply bind
  
  
 calls a method of an object,substituting another object for the current object
 
    const wizard={
    name='merlin',
    health='50',
    heal(){
    return.this.health=100;
    }
    }
    const archer={
    name:'robin hood',
    health:'30'
    }
    wizard.heal.call(archer)
    
 ->result 100
 we can also give parameter.in apply it takes parametet.example is given below:
 
 
    const wizard={
    name='merlin',
    health='50',
    heal(num1,num2){
    return this.health+=num1+num2;
     }
    }
    
    const archer={
    name:'robin hood',
    health:'30'
    }
    wizard.heal.apply(archer,[100,30])
    
 result->160
        
       const wizard={
    name='merlin',
    health='50',
    heal(num1,num2){
    return this.health+=num1+num2;
     }
    }
    
    const archer={
    name:'robin hood',
    health:'30'
    }
    const healarcher=wizard.heal.bind(archer,100,30)
    hearcher();
  bind is use for further use.
  
  
 ### context vs scope
 context is most often determine by how a function is invoked with the value of this keyword scope referes to the visibility of variable.
 
 
 
 ### learn from 3
     1.execution context
     2.lexical environment
     3.scope chain
     4.hoisting
     5.function invocation
     6.function scope vs block scope
     7.dynamic vs lexical scope
     8.this->call,apply,bind
     9.IIFE
  
  
  
  metarial :https://spin.atomicobject.com/2014/10/20/javascript-scope-closures/
  
  
  
  #### section overview
  
      topic: 1.closures
             2.prototype inheritance
for understanding two topic need clear concept in

     1.Higher order functions
     2.function vs object
     3.schema+java
     
lets learn this topic (: (: 

### higher order function
that can take a function as a argument or a function that returns another function


### closures

two benifits
1.memory efficient
2.encapsulation 

    const array=[1,2,3,4]

     for(var i=0; i<array.length; i++){

       setTimeout(() => {
          console.log(i);
       }, 300);
     }
 result will be->4444
 
 demonstrating that the loop and the timeout are running independently, and that by the time the first (and subsequent) setTimeout() function has run its code, the loop has already completed, leaving i set at 5.
 WAT!!! Why isn’t the output 1 2 3 4? There’s actually a lot going on in this subtle example.
 The short answer is that the for loop executes first, then it looks for the i value, which is 5, and then outputs four times, one for each loop iteration.Consider that even if we use a setTimeout of 0, the result is still the same.
 
    for (var i = 1; i < 5; i++) {
    setTimeout(() => console.log(i), 0)  // 5 5 5 5
    }
    
   .......JavaScript runtime engine........
   
   
   JavaScript runs within a browser and browsers do a lot more than just execute code. In fact, there are four distinct parts of the browser to consider:
   
       1 JavaScript runtime engine
       2 web APIs provided by the browser like the DOM, setTimeout, etc.
       3 a callback queue for events with callbacks like onClick and onLoad
       4 an event loop
   
 The runtime engine is what executes our code and each major browser has a slightly different engine under the hood. For example Chrome uses the V8 engine which also happens to power NodeJs. This engine can only execute one piece of code at a time.Web APIs are provided to us by the browser and include methods like setTimeout().These APIs are run independently, in a separate process, by the browser. This is how asynchronous JavaScript happens!!! It’s not that JavaScript itself is doing multiple things at once; instead the browser can run multiple different processes for us. runtime engine and the Web API interact using callback queue event loop.
 
 The setTimeout function can access the value of i because of closure. We ask for i within our console.log statement, but its value is set in an outer, enclosing scope, that of the for loop. Since inner functions have access to variables in an outer function, we are able to go up a level and retrieve the value of i, which is 5.
 
 
 
 
 
 
 
 we need to use let i=0,because var is global but let is block scope.
 
 or---
          
    const array=[1,2,3,4]
     for(var i=0; i<array.length; i++){

       (function(i){
          setTimeout(() => {
             console.log(i);
          }, 300);
       })(i)

     }
    
result->0 1 2 3





### oop

###  prototypal inheritance

    const elfFunction={

    attack(){

    return 'attack with'+this.weapon;
    }
    }


    function createElf(name,weapon){
    let newElf = Object.create(elfFunction)

      newElf.name=name,
      newElf.weapon=weapon;
      return newElf;
      
  
    }
    const peter=createElf("peter","x")

    console.log(peter.attack());

### constucors function


    function Elf(name,weapon){
       this.name=name;
       this.weapon=weapon
    }

    Elf.prototype.attack=function(){


       return 'attack with'+this.weapon;
    }
    const peter=new Elf('sam','fire');
    const sam=nwe Elf("x","y")
    console.log(peter.attack());


we are able to use this prototype to add fuctionality.we also able to use constuctor functions insted of something like object.create , to create a new object,return a new object  and also modifies what this means to whatever object call us so insted of the global object this is now point to the calling object peter and sam.But this a constuctor function we also have a prototype property that we can attach things to so that when peter dot attack gets called well peter dosen't have attack as it's own method but its going to go up the prototype chain .this prototype is going to have the attack and now both peter and sam are able to use attack from the same location in memory insted of us copying attack multiple places in multiple locations in memory.we just have it written once in memory and both of these else are going to point attack which is in the same memory space. 
