Execution Context is created in 2 phases-
### Creation Phase

  - JavaScript will allocate memory to all variables and functions
    Example -
    ```javascript
    var n = 2;

	function square(num){
		var ans = num*num;
		return ans;
	}
	var s2 = square(n);
	var s1 = square(1);
```
Creation Steps - 
1. on line 1 ->  ``` var n = 2; ```
   memory allocated to n - 

| Memory        | Code |
| ------------- | ---- |
| n : undefined |      |
2. on line 2 - 
```
   function square(num){
		var ans = num*num;
		return ans;
	}
```

<span style="color:rgb(255, 255, 0)">for variables -> special value undefined is stored in memory</span>
<span style="color:rgb(255, 255, 0)">for functions -> function definition is stored</span>

| Memory                                                                       | Code |
| ---------------------------------------------------------------------------- | ---- |
| n: undefined                                                                 |      |
| Square: function square(num){<br>		var ans = num*num;<br>		return ans;<br>	} |      |
3. for function calls lines
```
	var s2 = square(2);
	var s1 = square(1);
```


| Memory                                                                       | Code |
| ---------------------------------------------------------------------------- | ---- |
| n: undefined                                                                 |      |
| Square: function square(num){<br>		var ans = num*num;<br>		return ans;<br>	} |      |
| s2: undefined                                                                |      |
| s1: undefined                                                                |      |

###  Code Execution Phase

Now JS engines runs through the whole code again and starts execution line by line
1. on line 1 ->  ``` var n = 2; ```
   value of n is stored as 2 at this point -> undefined is replaced to 2

| Memory | Code |
| ------ | ---- |
| n : 2  |      |
2. on line 2 - 
```
   function square(num){
		var ans = num*num;
		return ans;
	}
```
There is nothing to execute in current context for JS on line 2 so it jumps to next line
```
	var s2 = square(2);
	var s1 = square(1);
```

<span style="color:rgb(146, 208, 80)">Function invocation</span>
- functions in JS are like a mini program - so whenever a function is invoked then a <span style="color:rgb(192, 0, 0)">completely new execution context is created</span>.

![[Pasted image 20240722125105.png]]


so new execution context is for this function scope - consider it being a mini program

Execution context for this code - >
```
   function square(num){
		var ans = num*num;
		return ans;
	}
```

step 1 - creation phase -> memory allocated for all the variables and functions including parameters to a function

| Memory         | Code |
| -------------- | ---- |
| num: undefined |      |
| ans: undefined |      |
step2 - code execution-
function call -> ```square(n)``` -> this passes n = 2 value to function ``` square ```
and executing num * num -> and storing value of 4 into ans

| Memory | Code      |
| ------ | --------- |
| num: 2 | num * num |
| ans: 4 |           |
<span style="color:rgb(192, 0, 0)">Return</span>  keyword returns control back to the execution context where it was invoked
return 4 to ```square2```  in above example
now execution context is 


| Memory                                                                       | Code |
| ---------------------------------------------------------------------------- | ---- |
| n: 2                                                                         |      |
| Square: function square(num){<br>		var ans = num*num;<br>		return ans;<br>	} |      |
| s2: 4                                                                        |      |
| s1: undefined                                                                |      |
when a function execution completes then whole execution context for that function instance gets deleted
![[Pasted image 20240722150528.png]]
At the end of execution of above program -> this is how different execution context were created
![[Pasted image 20240722150842.png]]



In the end when program complete the whole execution context is deleted 
![[Pasted image 20240722150951.png]]

## CallStack
Callstack maintain the <span style="color:rgb(146, 208, 80)">order of execution</span> of execution contexts
- It is stack where first execution context or the element at bottom is GEC(Global execution context) - whenever any JS programs start running this callstack is pre populated with GEC
  ![[Pasted image 20240722151430.png]]
- whenever a new execution context is created or function is invoked then that new execution context is pushed into the stack 
![[Pasted image 20240722151614.png]]
Let's consider new execution context as E1

![[Pasted image 20240722151709.png]]
- Once the execution of function completes then E1 is popped out from the stack  and Control goes back to GEC(or the top execution context on Stack currently)
  
![[Pasted image 20240722151824.png]]
After complete program execution completes -  call stack will be empty

