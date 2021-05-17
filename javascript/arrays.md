 ## javaScript Workshop topics
 ### JavaScript arrays

JavaScript has no built-in general map type (sometimes called associative array or dictionary) which allows to access arbitrary values by arbitrary keys. JavaScript's fundamental data structure is the object, a special type of map which only accepts strings as keys and has special semantics like prototypical inheritance, getters and setters and some further voodoo.

When using objects as **maps**, you have to remember that the key will be converted to a string value via **`toString()`**, which results in mapping 5 and '5' to the same value and all objects which don't overwrite the **toString()** method to the value indexed by '[object Object]'. You might also involuntarily access its inherited properties if you don't check hasOwnProperty().

JavaScript's built-in array type does not help one bit: JavaScript arrays are not associative arrays, but just objects with a few more special properties. If you want to know why they can't be used as maps

👉 Objects allow you to store keyed collections of values. 

But quite often we find that we need an ordered collection, where we have a 1st, a 2nd, a 3rd element and so on. For example, we need that to store a list of something: users, goods, HTML elements etc.

It is not convenient to use an object here, because it provides no methods to manage the order of elements. We can’t insert a new property “between” the existing ones. Objects are just not meant for such use.

🛑 There exists a special data structure named Array, to store ordered collections.

## Declaration
There are two syntaxes for creating an empty array:

```js
let arr = new Array();
let arr = [];
```

Almost all the time, the second syntax is used. We can supply initial elements in the brackets:

```js
let fruits = ["Apple", "Orange", "Plum"];
```
Array elements are numbered, starting with zero.

👆 We can get an element by its number in square brackets:

```js
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits[0] ); // Apple
alert( fruits[1] ); // Orange
alert( fruits[2] ); // Plum

```

👆 We can replace an element:

```js
fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]
```

👆 …Or add a new one to the array:

```js
fruits[3] = 'Lemon'; // now ["Apple", "Orange", "Pear", "Lemon"]
```
👆 The total count of the elements in the array is its length:

```js
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits.length ); // 3
```
👆 We can also use alert to show the whole array.

```js
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits ); // Apple,Orange,Plum
```

👉 An array can store elements of any type.

For example:

```js
// mix of values
let arr = [ 'Apple', { name: 'John' }, true, function() { alert('hello'); } ];

// get the object at index 1 and then show its name
alert( arr[1].name ); // John

// get the function at index 3 and run it
arr[3](); // hello
```

>Trailing comma
>An array, just like an object, may end with a comma:
>```js
>let fruits = [
>  "Apple",
>  "Orange",
>  "Plum",
>];
>```
>The “trailing comma” style makes it easier to insert/remove items, because all lines become alike.

👉 JavaScript arrays are objects. Objects have properties. A property name is a string value. Therefore, array indices are converted to strings as well before anything more can happen. A property name P will be treated as an array index (ie the special array-magic will be invoked) if the following holds (ECMA-262, 15.4):

>ToString(ToUint32(P)) is equal to P and ToUint32(P) is not equal to 2^32 − 1

That numeric indices will be converted to strings (and not the other way around) can be easily verified:

```js
let array = [];
array[1] = 'foo';
array['1'] = 'bar';
array['+1'] = 'baz';
document.writeln(array[1]); // outputs bar
```

Also, its bad practice to iterate over an array's entries with a `for..in` loop - you might get unexpected results if someone messed with some prototypes (and it's not really fast, either). Use the standard for `(let i= 0; i < array.length; ++i)` instead.



## 🛑 👆 Array methods

**concat**

>The **`concat()`** method is used to join two or more strings. This method does not change the existing strings, but returns a new string containing the text of the joined strings.

👉 Because the concat() method is a method of the String object, it must be invoked through a particular instance of the String class.

Syntax
In JavaScript, the syntax for the concat() method is:
```js
string.concat(value1, value2, ... value_n);
```

> 👆 Parameters or Arguments
value1, value2, ... value_n
The values to concatenate to the end of string.


Here are 2 ways to combine your arrays and return a NEW array. I like using the Spread operator. But if you need older browser support, you should use Concat.

```js
// 2 Ways to Merge Arrays

const cars = ['🚗', '🚙'];
const trucks = ['🚚', '🚛'];

// Method 1: Concat
const combined1 = [].concat(cars, trucks);

// Method 2: Spread
const combined2 = [...cars, ...trucks];

// Result
// [ '🚗', '🚙', '🚚', '🚛' ]
```

👉 Alternative Concat Syntax
Alternatively, you can also write the **concat method**, in this regard:

```js
const cars = ['🚗', '🚙'];
const trucks = ['🚚', '🚛'];

const combined = cars.concat(trucks);
// [ '🚗', '🚙', '🚚', '🚛' ]

console.log(cars); // ['🚗', '🚙'];
console.log(trucks); // ['🚚', '🚛'];
```

As you can see, this way of writing it doesn't manipulate or change the existing array.

Which one should I pick?

Let's list out both versions, so you can see it in comparison.

```js
// Version A:
const combinedA = [].concat(cars, trucks);

// Version B:
const combinedB = cars.concat(trucks);
```
So now the question is, which one should I pick 🤔. I prefer Version A because I think the intention is a lot more clear. Just by looking at it, I know I'm creating a new array and I'm not manipulating the existing array. Whereas if I look at Version B, it appears like I'm adding the trucks array to the cars array, and it doesn't seem obvious to me that the cars array isn't being changed. But, maybe that's just me. I'd be curious to know what you think?

## Difference between Spread vs Concat
I prefer using **`spread`**, because I find it more concise and easier to write. BUT, there are still benefits of using **`concat`**.

**Spread** is fantastic when you know beforehand that you're dealing with **arrays**. 
🤔 But what happens when the source is something else, like a **string**. And you want to add that string to the array. Let's walk through an example.

# 
Example: Dealing with an arbitrary argument
Let's say this is the outcome we want:

```js
[1, 2, 3, 'random'];
```

A. Using Spread

And if we follow the pattern we've been using and used the spread operator. Here's what happens:

```js
function combineArray(array1, array2) {
  return [...array1, ...array2];
}

const isArray = [1, 2, 3];
const notArray = 'random';

combineArray(isArray, notArray);
// 😱 [ 1, 2, 3, 'r', 'a', 'n', 'd', 'o', 'm' ]

```

☝️ If we spread our string, it will split the word into separate letters. So it doesn't achieve the result we want.

B. Using Concat

BUT, if we follow the concat pattern that we've been doing. Here's what happens:

```js
function combineArray(array1, array2) {
  return [].concat(array1, array2);
}

const isArray = [1, 2, 3];
const notArray = 'random';

combineArray(isArray, notArray);
// ✅  [ 1, 2, 3, 'random' ]
```

So here's the rule. If you know you're dealing with **`arrays`**, use **`spread`**. But if you might be dealing with the possibility with a non-array, then use concat to merge an array 👍

👉 use the most appropriate method depending on the problem you're trying to solve 👍


## - join() 

## 👆 push()

Append the element to the end of the array:

```js
let fruits = ["Apple", "Orange"];

fruits.push("Pear");

alert( fruits ); // Apple, Orange, Pear
```
The call `fruits.push(...) is equal to fruits[fruits.length] = ...`.



🛑 A queue is one of the most common uses of an array. In computer science, this means an ordered collection of elements which supports two operations:

`push`  - appends an element to the end

## 👆 shift()

`shift`  - get an element from the beginning, advancing the queue, so that the 2nd element becomes the 1st.

👆 Arrays support both operations.

In practice we need it very often. For example, a queue of messages that need to be shown on-screen.

There’s another use case for arrays – the data structure named [stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)).

It supports two operations:

push adds an element to the end.
pop takes an element from the end.
So new elements are added or taken always from the “end”.

👉 A stack is usually illustrated as a pack of cards: new cards are added to the top or taken from the top

👆 For stacks, the latest pushed item is received first, that’s also called LIFO (Last-In-First-Out) principle. For queues, we have FIFO (First-In-First-Out).

Arrays in JavaScript can work both as a **queue** and as a **stack**. They allow you to add/remove elements both to/from the beginning or the end.

In computer science the data structure that allows this, is called deque.


## 👆 pop()
Methods that work with the end of the array:

Extracts the last element of the array and returns it:

```js
let fruits = ["Apple", "Orange", "Pear"];

alert( fruits.pop() ); // remove "Pear" and alert it

alert( fruits ); // Apple, Orange
```

## 👆 UnShift()


Add the element to the beginning of the array:

```js
let fruits = ["Orange", "Pear"];

fruits.unshift('Apple');

alert( fruits ); // Apple, Orange, Pear
```

👉 Methods `push` and `unshift` can add multiple elements at once:

```js
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

// ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
alert( fruits );
```

## 👆 sort()

In JavaScript, we can sort the elements of an array easily with a built-in method called the sort( ) function.

```js
const teams = ['Real Madrid', 'Manchester Utd', 'Bayern Munich', 'Juventus'];
```
When we use the sort( ) method, elements will be sorted in ascending order (A to Z) by default:
```js
teams.sort(); 

// ['Bayern Munich', 'Juventus', 'Manchester Utd', 'Real Madrid']
```
If you prefer to sort the array in descending order, you need to use the reverse( ) method instead:

```js
teams.reverse();

// ['Real Madrid', 'Manchester Utd', 'Juventus', 'Bayern Munich']
```
## Array of Numbers

👉 Sorting numbers is unfortunately not that simple. If we apply the sort method directly to a numbers array, we will see an unexpected result:

```js
const numbers = [3, 23, 12];

numbers.sort(); // --> 12, 23, 3
```
🤔 Why the `sort( )` method isn't working for numbers?
Actually it is working, but this problem happens because JavaScript sorts numbers alphabetically. Let me explain this in detail.

👉 Let's think of A=1, B=2, and C=3.

```js
const myArray = ['C', 'BC', 'AB'];

myArray.sort(); // [AB, BC, C]
```

As an example, if we have three strings as C (3), BC (23) and AB(12), JavaScript will sort them as AB, BC, and C in an ascending order, which is alphabetically correct.

## The Compare Function is a solution

the `sort( )` method can be supported with a basic comparison function which will do the trick:

```js
function(a, b) {return a - b}
```

The `sort` method, fortunately, can sort negative, zero, and positive values in the correct order. When the `sort( )` method compares two values, it sends the values to our compare function and sorts the values according to the returned value.

>👉 If the result is negative, a is sorted before b.

>👉 If the result is positive, b is sorted before a.

>👉 If the result is 0, nothing changes.

**All we need to is using the compare function inside the `sort( )` method:*

```js
const numbers = [3, 23, 12];

numbers.sort(function(a, b){return a - b}); // --> 3, 12, 23

```
If we want to sort the numbers in descending order, this time we need to subtract the second parameter (b) from the first one (a):
```js
const numbers = [3, 23, 12];

numbers.sort(function(a, b){return b - a}); // --> 23, 12, 3
```



## slice()

## 👆 splice()