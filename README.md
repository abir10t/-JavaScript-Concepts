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

    Elf.prototype.build=function()
    {
    const self=this
    function building(){
        return self.name
     }
     return building();
    }
  function inside of a function ,that means this is not assigned to the object itself but actually to the window object. so solution is  const self=this.
  
    function Elf(name,weapon){
       this.name=name;
       this.weapon=weapon
    }
   if we want to declear a variable we need to use this keyword .
   
   this constuctor way is not pretty.now we improve this......!!!
     
    class Elf{
       constructor(name,weapon){
       this.name=name;
       this.weapon=weapon                    //use this way ******
       }
    attack(){
       return 'attack with'+this.weapon;
       }
    }

    const peter=new Elf('sam','fire');

    console.log(peter.attack());

   thats the way.this is not oop .this is waht we call syntactic sugar underneath the hood in javascript we are still using prototype all inheritance.we are not using classes like classes work in other language.this is the closest that js is going to get to classes. undrneath the hood they are still using the new keyword with the prototype.in js classes are object,so if somone questio->does js have classes ->well ,yes ,they do as syntactic sugar but class keyword is still just prototype all inheritance.some people call this pseudo classical inheritance because its not classical inheritance..
why we put attack() outside? every time we use the new keyword and create or instantiate a class the constuctor function gets run because each elf has a unique name and perhaps a unique weapon,but attack is shared by all instances of the class if we moved attack to the constuctor thats going to take up memory space.js, is weird :p :p 

# this->
    1 new binding
    unction Person(name,age){
    this.name=name;
    this.age=age;
    }
    const person1=new Person("a","b")
    
    2.implicit binding
    const person={
    name:'karim',
    hi(){
    console.log('hi'+this.name)
     }
    }
    
    3.explicit binding
    const person3={
       name:'karen',
       age:40,
       hi:function(){
          console.log('hi'+this.setTimeout)
       }.bind(window)
    }
in hi funcation there is a set timeout.if we want to refer to the window object we can explicitly tell it what to bind to .and we say bind to window.
    
    4. arrow funcation
            const person4={
       name:'karen',
       age:40,
       hi:function(){
          var inner=()=>{
             console.log('hi'+this.name)
          }
        return inner()
       }
    }
    console.log(person4.hi())
   
 here inside of hi function has a another function.a method with a function inside of it is the biggest gotacha when it comes to this.well if we run inner here and we run it everything is working because we are using arrow function if
 we didn't used a regular function well in that case this would be the window object .which we usually never want.

        
 ### inheritance
     class Character{
       constructor(name,weapon){
       this.name=name;
       this.weapon=weapon                   
       }
    attack(){
       return 'attack with'+this.weapon;
       }
    }


    class Ogre extends Character{

       constructor(name,weapon,color)
       {
          super(name,weapon)
          this.color=color;
       }
       makeFort()
       {
          return 'strong fronrt';
       }
    } 
    const dolby=new Ogre('x','y','z');

    ....... pillars of oop ..........
            1.encapsulation
               2.abstraction
                   3.inheritance
                       4.polymorphism
                       
 ### functional programming
    1.curry
    2.partial Application
    3.pure Functions
    4.Referential Transparency
    4.compose
    5.pip
    
 ### pure function
 
pure function is the pilar of functional programming.main two things is -> a function has to always return the same output given the same input,and the function can't modify anything outside of itself(no side effect).
....side effect...

    onst array=[1,2,3]
    function mutateArray(arr)
    {
    arr.pop()
    }
    a(array);      ///1,2
    
 mutateArray(arr) this function has side effects.the function modify anything outside of itself.and it does,modify array[1,2,3]that lives outside pof itself in the global object and this is called a side effect.
 
    
    const array=[1,2,3]
    function x(arr)
    {
     const newArray=[].concat(arr);
     newArray.pop();
     return newArray
    }
    function multiplyby2(arr){
       return arr.map(item=>item*2)
    }
    console.log(x(array));  //1,2
    console.log(array)     //1,2,3
    console.log(multiplyby2(array)) //2,4,6
    console.log(array) //1,2,3
    
  this function has no site effect and if we give same input we will find same output ..so it's pure function
  ..... in the end we tell that,we can't make a side effect code.
  
  
  ### idempotent
  
    
    function notGood(){


    return Math.random();
    }
    console.log(notGood());
  
we will get a random number between 0 and 1,and what independence means is that given the same inputs we will find different outputs.

### imperative vs Declarative 

### Immutability 
    const obj={name: 'Andrei'}
    function clone(obj){
    return {...obj};

    }
    console.log(obj.name='Nana')
    
   immutability means not changing the data not changing the state.In functional programming the idea of immutability is very important.we can change things inside of our function but we don't want to affects the outside world in our programs.
