### UnderscoreJS
    1. each: https://www.youtube.com/watch?v=FHfnbza1gUM
    
    
    
### primitive vs referance value :
1.

    let x=["sports"]
    let newx = x
    x.push("c")
    newx-> sports, c
    
    same in object. pointer concept
    

2. recover way
        
       obj-> let x={...name}
       arr-> let x=[...y]
       
3.

    const person1={age:30}
    const person2={age:32}
    person1 === person2 -> false, person1 and person 2 are save in different pointer
    
    
4.

    const hobbies=['sports']
    hobbies.push('cooking') -> we are just allocate more memory in same address, so thats possible in const variable
    hoibbies=['x','y','z']  -> that's not possible , we are making new address of hobbies.
    
5.
 
    const person = {age:30};
    person.age=32 -> here we just change the memory, so that's possible
    person={age:55} -> that's not possible, we are using new address
    
    
 ### Hoisting :
 
      console.log(userName)
      var userName="max" -> here username is undifined for hoistiing.in browser first "var username=undifined" makes. but let and const doesn't do that.
      
      
  ### Garbage collection & memory management :
        let person = {name:"max"} -> avobe statement is not necessary. So js engine garbage collector kick it out
        person = null; 
        
 ### best practrice to give a annonyomus function name. because in erron option we can find annonyomus function name & linwe number.
 
 
 ### arrow function :
    1. no arguments / parameters..............() => {...}
    2. Exactly 1 argument / parameters.................arg => {...}
    3. Exactly one expression in function body .......(a,b) => a+b  //here return works auto
    
    
    
 ### Rest operator:
 
    1. const sumUp = (...numbers) =>
       {
           let sum=0;
           for(const num of numbers){   // for (const num of arguments) here arguments is keyeord, we need to use " const x=function(){}, in argument we can't use arrow function.
                    sum +=num;
           
           }
           return sum;
       }
       
        console.log(sumUp(1,5,10,-3,-6,10) // we dont pass array because of rest operator. for 1,5 -> const sumUp = (a,b, ...numbers) =>
        
        
### callback function:

    const sum = (result, ...numbers) => {
       let sum = 0;

       const ch = (num) => {
          return isNaN(num) ? 0 : num

       };
       for (const num of numbers) {

          sum = sum + ch(num);
       }

       result(sum); // we transfer sum in the show funstion.
    };

    const show = (result) => {
       alert("the result after adding the" + result);
    };

    console.log(sum(show, 2, 3, 4)) // show is a parameter of sum function
    
    
 
 
### Exploring and Changing DOM Properties :

    
     1. <p id="welcome-text" class="text-default">welcome</p>
        const p = document.getElementById('welcome-text'); // for select a tag -> document.querySelector('h1')
        p.textContent -> welcome
        p.id -> welcome-text
        p.className ->"text-default" // the name that is occure in  css file 
     
     
     2. work with css:
       h1.style.color="white"
       
     3. search google -> mdn h1 element 
   
