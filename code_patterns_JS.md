# Table of contents:

* [ternary operator](#ternary-operator)
* [multiple logical operators](multiple-logical-operators)
* [nested arrow functions](nested-arrow-functions)
* [chaining promises](chaining-promises)
* [promise consecutive resolve](promise-consecutive-resolve)
* [assignment in arrow function](assignment-in-arrow-function)

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
