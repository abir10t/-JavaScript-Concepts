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
 var ,let,const tell js variable environment this is a variable .but here height=50 go to global scope chain 'use strict' can help this for not doing this kind of weird js.use it global.
 
 
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
    
    
    




