+++
date = "2018-05-15"
title = "Chunky Monkey Algorithm Challenge🐒"

+++

Today I was able to solve what in reality is a basic Javascript algorithm. For those of you who are more experienced with coding, this algorithm will be easy, but for me, it was a fun challenge.  In this post I'll attempt to explain the steps that I (eventually) took to solve it. So buckle up buckaroos and join me on a coding journey.

![enter image description here](https://media.giphy.com/media/VNhrzGZDa8mZy/giphy.gif)


The Chunky Monkey algorithm is part of the [FreeCodeCamp Front-End Web Development Certification](https://www.freecodecamp.org). It required me to write a function that split an array (first argument, **arr**) into groups with lengths equal to the second argument (**size**) and then return them as a two-dimensional array (**newArr**). 

See below for the expected outputs using various arguments:

**Code Snippet 1**
```js
function chunkArrayInGroups(arr, size) {
  return newArr;
}
chunkArrayInGroups(["a", "b", "c", "d"], 2); 
// newArr = [["a", "b"], ["c", "d"]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 3); 
// newArr = [[0, 1, 2], [3, 4, 5]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 2); 
// newArr = [[0, 1], [2, 3], [4, 5]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 4); 
// newArr = [[0, 1, 2, 3], [4, 5]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3); 
// newArr = [[0, 1, 2], [3, 4, 5], [6]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 4); 
// newArr = [[0, 1, 2, 3], [4, 5, 6, 7], [8]]

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6, 7, 8], 2); 
// newArr = [[0, 1], [2, 3], [4, 5], [6, 7], [8]]
```

The first thing that I noticed is that there were two general classes of  outputs: 

- The first three function calls all resulted in sub-arrays that each contained the same number of elements.
- The other four function calls resulted in sub-arrays that did not all have the same number of elements.

The first sub-array of all function calls, however, all had lengths = **size**. These observations gave me an idea💡, maybe there was a relationship between the function arguments that I could exploit to construct the desired outputs. Other than datatype, which makes no difference, the only other obvious property of  **arr** that varied was its length (arr.length). Of course **size** also varied from example to example. 

In order to find that relationship I decided to write a simple function that divided **arr.length** by **size** and see what those outputs would yield: 

**Code Snippet 2**
```js
function test(arr, size){
	console.log(arr.length / size);
}
test(["a",  "b",  "c",  "d"],  2); //Output:  2
test([0,  1,  2,  3,  4,  5],  3); //Output: 2
test([0,  1,  2,  3,  4,  5],  2); //Output: 3
test([0,  1,  2,  3,  4,  5],  4); //Output: 1.5
test([0,  1,  2,  3,  4,  5,  6],  3); //Output: 2.33
test([0,  1,  2,  3,  4,  5,  6,  7,  8],  4); //Output: 2.25
test([0,  1,  2,  3,  4,  5,  6,  7,  8],  2); //Output: 4.5
```
Function calls 1-3 all yielded whole numbers where the output represented the number of sub-arrays present in **newArr** while **size** represented the number of elements in each sub-array when **chunkArrayInGroups** was called (See **Code Snippet 3**).


**Code Snippet 3**

```js
function chunkArrayInGroups(arr, size) {
  return newArr;
}

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 3); 
// Output: [[0, 1, 2], [3, 4, 5]] // arr.length / size = 2
// 2 sub-arrays each containing 3 (size) elements

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 2); 
//Output: [[0, 1], [2, 3], [4, 5]] // arr.length / size = 3
// 3 sub-arrays each containing 2 (size) elements
```
Function calls 4-7 all yielded fractions. What I noticed is that whatever function I needed to create, would have to create as many sub-arrays with **size** number of elements in them, and then add the remaining element(s) to the final sub-array.  For function calls where arr.length / size = floating point, the final sub-array will contain a fraction of **size** number of elements (**See Code Snippet 4**)


**Code Snippet 4**

```js
function chunkArrayInGroups(arr, size) {
  return newArr;
}

chunkArrayInGroups([0, 1, 2, 3, 4, 5], 4); 
//Output: [[0, 1, 2, 3], [4, 5]] // arr.length / size= 1.5
// 2 sub-arrays, one containing size number of elements.
// The other containing (0.5 * size) elements

chunkArrayInGroups([0, 1, 2, 3, 4, 5, 6], 3); 
//Output: [[0, 1, 2], [3, 4, 5], [6]] // arr.length / size = 2.33
// 3 sub-arrays, two containing size number of elements
// Final array containing (0.33 * size) elements
```

With these clues in mind I then went about constructing and testing various functions.  I knew that I would have to iterate through **arr**  using a for loop. With each iteration of the loop I'd need to extract elements from **arr** and then add the extracted elements to a new two-dimensional array. I could achieve this by using the [push](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push) and [slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) methods. The number of iterations would determine the number of sub-arrays in **newArr**.  From my previous experimentation, I knew that the number of sub-arrays = (arr.length / size); at least for the first three function calls in **Code Snippet 2**. 

**Code Snippet 5**
```js
function chunkArrayInGroups(arr, size){
	var newArr =  [];
	for(var i =  0; i < arr.length/size; i++){
		newArr.push(arr.slice(?, ?));
	}
return newArr;
}
```

As you can see above, I need to determine what would be valid arguments for the slice method. The first argument represents the index of the first element to be passed into the sub-array. The second argument represents the index of the element up to which is sliced into the sub-array; that element itself not included in the sub-array. 

I decided to reverse engineer functions call 1-3 from **Code Snippet 1** to determine how those arguments needed to vary to give me my desired result:

**Code Snippet 6**
```js
function chunkArrayInGroups(arr, size){
	var newArr =  [];
	for(var i =  0; i < arr.length/size; i++){
		newArr.push(arr.slice(beginIndex,endIndex));
	}
return newArr;
}

//Function Call 1
chunkArrayInGroups(["a", "b", "c", "d"], 2); // [["a", "b"], ["c", "d"]]

//Function Call 2
chunkArrayInGroups([0, 1, 2, 3, 4, 5], 3); // Output: [[0, 1, 2], [3, 4, 5]]

//Function Call 3
chunkArrayInGroups([0, 1, 2, 3, 4, 5], 2); //Output: [[0, 1], [2, 3], [4, 5]]
```
**Function Call 1**
--
**size = 2**


| Loop Iteration | beginIndex | endIndex |
|----------------|------------|----------|
| 1              | 0          | 2        |
| 2              | 2          | 4        |


**Function Call 2**
--
**size = 3**

| Loop Iteration | beginIndex | endIndex |
|----------------|------------|----------|
| 1              | 0          | 3        |
| 2              | 3          | 6        |


**Function Call 3**
--
**size = 2**

| Loop Iteration | beginIndex | endIndex |
|----------------|------------|----------|
| 1              | 0          | 2        |
| 2              | 2          | 4        |
| 3              | 4          | 6        |


Two conclusions can be drawn from the tables above: 

1. **beginIndex** and **endindex** increase by **size** during each for loop iteration.

3. **endIndex** = **beginIndex** + **size**

Using this information, I created a variable, **count** that increases by  **size** during each iteration of the for loop and acts as the beginning index. The **endIndex** therefore becomes **count** + **size** based on the relationship described in the conclusion above.  

**Code Snippet 7**
```js
function chunkArrayInGroups(arr, size){
	var newArr =  [];
	var count = 0;
	for(var i =  0; i < arr.length/size; i++){
		newArr.push(arr.slice(count,count + size));
		count = count + size;
	}
return newArr;
}
```
The function above works!🎉🎉 You don't even have to take my word for it, give a go below🙏: 

<iframe height="400px" width="100%" src="https://repl.it/@akonobrathwaite/ChunkyMonkey-Blog-Post?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>

**NB**: You can comment out the function calls that you don't want to run.

You may have noticed that this function also works for the function calls where the final outputted sub-array was not the same length as the preceding sub-arrays. This was actually a bit of a mystery for me until I broke down what the final iteration of the for loop was doing. 

**Function Call 5**
**size = 3**

**Code Snippet 8**
```js
chunkArrayInGroups([0,  1,  2,  3,  4,  5,  6],  3);
//Output: [ [ 0, 1, 2 ], [ 3, 4, 5 ], [ 6 ] ]
```
Final iteration of for loop for Function Call 5

| Loop Iteration | beginIndex | endIndex |
|----------------|------------|----------|
| 3              | 6          | 9        |


This final iteration of the for loop extracts the element with index 6, up to, but not including the element with index 9. In this case **arr** does not contain an element with index 9. Because of this the slice method just extracts all remaining elements into the final sub-array. See the [MDN webdocs](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) for more information. 

So that's it! We've solved the Chunky Monkey Algorithm Challenge.🎆🎆 I hope that you've enjoyed this journey and have learned a thing or two 😉