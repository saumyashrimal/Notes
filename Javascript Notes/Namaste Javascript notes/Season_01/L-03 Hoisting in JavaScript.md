What is Hoisting ??
Hoisting is phenomenon in JS which let's you access variables and function before even they are initialised with a value without getting any error
Example Code 
```javascript
var name = 'saumya'

function getName(){
	console.log("name is ");
}

console.log(name) // prints saumya
console.log(getName) // prints function getName definition
```

what if those 2 console.log statements are executed before name is initialised and function getName is defined.

```javascript

console.log(name) // prints undefined
console.log(getName) // prints function getName definition
getName() // print "name is "

var name = 'saumya'

function getName(){
	console.log("name is ");
}
```

- For most of the languages -> it would throw error if you try to invoke a function before it is defined but in javascript it is different
- Remember execution context and it's 2 phases -> creation phase (memory allocation phase)
  so before even JS starts executing the code line by line, memory allocation phase is already completed and the variable are assigned undefined in execution context and function are assigned with their definition in execution context
  
Let's see how it is working in browser env
1. putting debugger on the first line of code so execution is not even started yet 
![[Pasted image 20240722155607.png]]

getName function definition is stored in GEC even before code execution starts
![[Pasted image 20240722155834.png]]


## Difference between Not Defined and Undefined

- Not Defined 
when there is no variable present in current execution context then you get the reference error or Not defined

```javascript
console.log(x) // throws error -> ReferenceError: x is not defined
console.log(getName) // prints function getName definition

function getName(){
	console.log("name is ");
}
```
As x variable is not available in memory or GEC or current context so JS throws Reference Error as x is not defined

- Undefined - undefined acts as a placeholder or the values which are not initialised at the time of execution but has a memory allocated in execution context

### Arrow Functions hoisting

```javascript
console.log(getName) // prints undefined
getName() // throws Error -> TypeError: getName is not a function

var getName = () => {
	console.log("name is ");
}
```
getName is treated here as a variable until initialised and for all uninitialised variables the value is undefined

![[Pasted image 20240722161329.png]]