# Table of contents:

* [ternary operator](#ternary-operator)
* [multiple logical operators](#multiple-logical-operators)
* [nested arrow functions](#nested-arrow-functions)
* [chaining promises](#chaining-promises)
* [promise consecutive resolve](#promise-consecutive-resolve)
* [assignment in arrow function](#assignment-in-arrow-function)
* [HTML tag with multiple attributes](#multiple-element-attributes)
* [Guard Pattern](#guard-pattern)
* [Wrapping promises](#wrapping-promises)

# Basics

## Ternary operator <a id='ternary-operator' href='#ternary-operator'>&#9875;</a>

```javascript
return (doSomeCalculation() === 1) 
  ? doWhenTrue()
  : doWhenFalse();
```

## Multiple logical operators in statement <a id='multiple-logical-operators' href='#multiple-logical-operators'>&#9875;</a>

```javascript
return isItTrue() 
  && (isItTrueAlso1() || isItTrueAlso2())
  && returnIfAllTrue;
```

```javascript
return isItTrue() 
  && (isItTrueAlsoVeryLongStatementWithManyLetters1() 
    || isItTrueAlsoVeryLongStatementWithManyLetters2())
  && returnIfAllTrue;
```

## Nested arrow functions <a id='nested-arrow-functions' href='#nested-arrow-functions'>&#9875;</a>

```javascript
const returnFunc = () => 
  someData => (doSomeCalculation() === 1)
    ? 'RETURNED_IF_TRUE'
    : 'RETURNED_IF_FALSE';
```

## Chaining promises <a id='chaining-promises' href='#chaining-promises'>&#9875;</a>

```javascript
const add1ToVal = val => val + 1;
const add2ToVal = val => val + 2;

const returnPromise()
  .then(add1ToVal)
  .then(add2ToVal)
  .then(() => finalResolve());
```

## Resolving promises consecutive (without async await) <a id='promise-consecutive-resolve' href='#promise-consecutive-resolve'>&#9875;</a>

* with resultat of previous one 

```javascript
const promises = [promise1, promise2, promise3];

return promises
  .reduce((promise, currentPromise) => 
    promise.then(currentPromise), Promise.resolve());
```
* without resultat of previous one

```javascript
const promises = [promise1, promise2, promise3];

return promises
  .reduce((promise, currentPromise) => 
    promise.then(() => currentPromise()), Promise.resolve());
```

## Assignment in arrow function <a id='assignment-in-arrow-function' href='#assignment-in-arrow-function'>&#9875;</a>
```javascript
const object = {};
...
.then(val => { object.val = val; }); 
```

better:

```javascript
const object = {};
...
.then(val => Object.assign(object, val)); 
```

best:

```javascript
const object = {};
...
.then(val => Object.assign({}, object, val)); 
```

## HTML tag with multiple attributes <a id='multiple-element-attributes' href='#multiple-element-attributes'>&#9875;</a>

### Do always, when more than 2 attributes

bad:
```javascript
<input id='someDiv' class='someClass' name='someName' type='text' placeholder='type text'>
```
good:
```javascript
<input id='someDiv' 
       class='someClass' 
       name='someName' 
       type='text' 
       placeholder='type text'>
```

## Guard pattern <a id='guard-pattern' href='#guard-pattern'>&#9875;</a>

Bad:
```javascript
(value) => {
  if (value) {
    return doSthgWithValue(value)
      .then(modifiedValue => `Returned value: ${modifiedValue}`);
  }
};
```
Better:
```javascript
(value) => {
  if (value) {
    return doSthgWithValue(value)
      .then(modifiedValue => `Returned value: ${modifiedValue}`);
  }
  return Promise.resolve(null); // or Promise.reject(Error(...)) depending on circumstances
};
```
Good:
```javascript
(value) => {
  if (!value) {
    return Promise.resolve(null); // or Promise.reject(Error(...)) depending on circumstances
  }
  return doSthgWithValue(value)
    .then(modifiedValue => `Returned value: ${modifiedValue}`);
};
```
It is the best practice to use guard pattern always, especially, when we require specific response type. In first example there were two types of function interface depending on input: `Promise` (when successful check) and `undefined` (returned as default by function in JS), which could cause Errors like: `.then(...) is not a function` or other caused by returning undefined instead of Promise.
That's good practise too, when the interfaces wouldn't be much different. Consider following case:
```javascript
(value) => {
  if (value) {
    const firstString = 'First part of string';
    const secondString = 'Second part of string';

    return `${firstString}; ${secondString}; Value: ${value}`;
  }
};
```
in this case, function will return string if value, and undefined of not, but it's not explicitly said. It is much clearer what function does, when we write it as follows:
```javascript
(value) => {
  if (value) { return ''; }

  const firstString = 'First part of string';
  const secondString = 'Second part of string';

  return `${firstString}; ${secondString}; Value: ${value}`;
};
```
not only function has unified output, but it also doesn't require nesting correct function activity.

The benefits of guard pattern are even better seen in more complicated examples.
Instead of nested 'if-else's:
```javascript
({ firstVal, secondVal, lastVal}) => {
  if (firstVal) {
    const firstString = `FirstVal: ${firstVal}`;

    if (secondVal) {
      const secondString = `SecondVal: ${secondVal}`;

      if (lastVal) {
        const lastString = `LastVal: ${lastVal}`;

        return `${firstString}, ${secondString}, ${lastString}`;
      } else {
        return `${firstString}, ${secondString}`;
      }
    } else {
      return `${firstString}`;
    }
  } else {
    return '';
  }
};
```
we can write it as:
```javascript
({ firstVal, secondVal, lastVal}) => {
  if (!firstVal) { return ''; }

  const firstString = `FirstVal: ${firstVal}`;

  if (!secondVal) { return `${firstString}`; }

  const secondString = `SecondVal: ${secondVal}`;

  if (!lastVal) { return `${firstString}, ${secondString}`; }

  const lastString = `LastVal: ${lastVal}`;

  return `${firstString}, ${secondString}, ${lastString}`;
};
```

## Wrapping promises <a id='wrapping-promises' href='#wrapping-promises'>&#9875;</a>

Good practise in writing code based at some point on promises is using just one type of promises, one interface, one library, but not always you are able to choose which promises will be used by library, you're using. Especially, when those  libraries use promises with poorer interface. That's when helpful is promises wrapping. Promises wrapping is just a functionality of promises, which helps unify interfaces.

E.g. when you're using bluebird in your code and one of your lobraries is using natie Promises, you can just:

```javascript
const bluebird = require('bluebird');
const lib = require('lib');

lib.doSthAsync()
  .then() // interface of promises used by lib
  
bluebird.resolve(lib.doSthAsync())
  .then() // interface of bluebird
  .map()
  .filter() // ...

```
