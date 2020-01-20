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
    
    
 2.ececute same code for multiple object
    
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




