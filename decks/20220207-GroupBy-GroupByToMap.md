---
title: GroupBy and GroupByToMap
date: 07.02.2022
author: Oriol Torrent Florensa
description: 2 new methods for Array
separator: <!--h-->
verticalSeparator: <!--v-->
notesSeparator: <!--n-->
theme: blood
css: ./custom/styles/general.css
template: ./custom/templates/general.html
revealOptions:
    transition: 'fade'
---

# GroupBy and GroupByToMap
<!-- .element: class="r-fit-text" -->

2 new methods for Array

<!--h-->

- GroupBy: `array.groupBy(callback, thisArg?)`
- GroupByToMap: `array.groupByToMap(callback, thisArg?)`

Currently, at Stage 3 (out of 4)
<!-- .element: class="fragment" -->

<!--n-->
The TC39 process: https://tc39.es/process-document/
<br />
Stage 3 indicates that further refinement will require feedback from implementations and users


<!--h-->

## Introduction

- Both methods belong to the same proposal: https://github.com/tc39/proposal-array-grouping
- Both methods will be used to *group* Arrays
- Both iterate over the Array and applies the provided callback function

<!--v-->

- Each method returns differently:
    - `GroupBy`: Given a callback function that returns arbitrary strings, `GroupBy` **returns an Object** that stores the group members as values in the given arbitrary keys from the callback function
    - `GroupByToMap`: Given a callback function that returns arbitrary Map keys, `GroupByToMap` **returns a Map** that stores the group members as Map values in the given arbitrary map keys from the callback function

<!--n-->
Remember: A Map's keys can be any value (including functions, objects, or any primitive): https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map#objects_vs._maps


<!--h-->

## GroupBy

```js
const array = [1, 2, 3, 4, 5];

// groupBy groups items by arbitrary key.
// In this case, we're grouping by even/odd keys

array.groupBy((num, index, array) => {
	return num % 2 === 0 ? 'even': 'odd';
});

// { 'odd': [1,3,5], 'even': [2,4] }
```

<!--v-->

### `GroupBy` example

```js
const groupBySign = nums => nums.groupBy(elem => {
	if (elem < 0) {
		return 'negative';
	} else if (elem === 0) {
		return 'zero';
	} else {
		return 'positive';
	}
});

assert.deepEqual(
	groupBySign([0, -5, 3, -4, 8, 9]),
	{
		__proto__: null,
		zero: [0],
		negative: [-5, -4],
		positive: [3, 8, 9],
	}
);
```

<!--n-->
Notice that the prototype of the object returned by .groupBy() is `null`. That makes it a better dictionary because no properties are inherited and the property __proto__ does not have any special behavior.

<!--v-->

### `GroupByToMap` example

```js
// groupByToMap returns items in a Map, and is useful for grouping using an object key.
const odd  = { odd: true };
const even = { even: true };

array.groupByToMap((num, index, array) => {
	return num % 2 === 0 ? even: odd;
});

// Map { {odd: true}: [1, 3, 5], {even: true}: [2, 4] }
```

<!--h-->

## Use cases

- Grouping by known keys ahead of time
    - *we are interested in the **values** of each case*
- Grouping by property values from unknown keys
    - *we are interested in the **key-value pairs***
- Counting members of the groups
    - *we're interested in the **amount of values** of the resulting key-value pairs*

<!--v-->

### Grouping by known keys

Given several Promises to fetch users:

```js
const settled = Promise.allSettled([promise1, promise2, …etc]);
/*
[
	{ status: 'rejected', reason: 'Jhon' },
	{ status: 'fulfilled', value: 'Jane' },
	{ status: 'fulfilled', value: 'John' },
	{ status: 'rejected', reason: 'Jaen' },
	{ status: 'rejected', reason: 'Jnoh' },
];
 */
```

<!--v-->

We can group them by status as follows:

```js
const {fulfilled, rejected} = settled.groupBy(x => x.status);

/* fullfilled:
[
	{ status: 'fulfilled', value: 'Jane' },
	{ status: 'fulfilled', value: 'John' },
]
 */

/* rejected:
[
	{ status: 'rejected', reason: 'Jhon' },
	{ status: 'rejected', reason: 'Jaen' },
	{ status: 'rejected', reason: 'Jnoh' },
]
 */
```

<!--n-->
For this use case, .groupBy() works better because we can use destructuring


<!--h-->

### Grouping by property values

Given an array of users and their country:

```js
const users = [
  { name: 'Louise', country: 'France' },
  { name: 'Felix', country: 'Germany' },
  { name: 'Ava', country: 'USA' },
  { name: 'Léo', country: 'France' },
  { name: 'Oliver', country: 'USA' },
  { name: 'Leni', country: 'Germany' },
];
```

<!--n-->
Note that we cannot preview neither users' names nor countries' names

<!--v-->

We can group them by country as follows:

```js
users.groupByToMap(user => user.country);

/*
new Map([
	[
		'France',
		[
			{ name: 'Louise', country: 'France' },
			{ name: 'Léo', country: 'France' },
		]
	],
	[
		'Germany',
		[
			{ name: 'Felix', country: 'Germany' },
			{ name: 'Leni', country: 'Germany' },
		]
	],
	[
		'USA',
		[
			{ name: 'Ava', country: 'USA' },
			{ name: 'Oliver', country: 'USA' },
		]
	],
]);
 */
```

<!--v-->

Then we can see the users from France like follows:

```js
userByMap.get('France');

/*
[
	{
		"name": "Louise",
		"country": "France"
	},
	{
		"name": "Léo",
		"country": "France"
	}
]
 */
```

<!--n-->
For this use case, .groupByToMap() is a better choice because we can use arbitrary keys in Maps whereas in objects, keys are limited to strings and symbols.


<!--h-->

### Counting elements

Given an array of unknown elements:

```js
const words = text.split(' ');
```

<!--v-->

We count how often each word occurs in a given text:

```js
function countWords(text) {
	const words = text.split(' ');
	const groupMap = words.groupByToMap((word) => word);
	return new Map(
		Array.from(groupMap) // (A)
			.map(([word, wordArray]) => [word, wordArray.length])
	);
}
```

<!--n-->
we take a detour via an Array because Maps don’t have a method .map().

<!--v-->

```js
countWords('knock knock chop chop buffalo buffalo buffalo')

/*
new Map([
	['buffalo', 3],
	['chop', 2],
	['knock', 2],
]);
 */
```

<!--n-->
We are only interested in the sizes of the groups.


<!--h-->

## Grouping Array elements to multiple groups?
<!-- .element: class="r-fit-text" -->

For example, group articles by tags:

```js
const articles = [
	{title: 'Sync iteration', tags: ['js', 'iter']}, 
	{title: 'Promises', tags: ['js', 'async']},
	{title: 'Async iteration', tags: ['js', 'async', 'iter']},
];
```

<!--v-->

⚠️ We cannot use the grouping methods if each element of the input Array can belong to multiple groups.

Then we have to write our own grouping function


<!--h-->

References:

- https://github.com/tc39/proposal-array-grouping
- https://2ality.com/2022/01/array-grouping.html
- https://dev.to/hypeddev/arrayprototypegroupby-in-javascript-1pd0

<!--h-->

Now go and change the world<br />💪🏼🌍👩🏻‍💻
<!-- .element: class="r-fit-text" -->

Happy conding! 😁👩🏻‍💻
