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
        
 ### need to give name of a anonymous function for finding error with line number and that anonymous function name. 
