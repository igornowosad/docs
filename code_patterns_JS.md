#Basics

## Ternary operator

```javascript
return (doSomeCalculation() === 1) 
  ? doWhenTrue()
  : doWhenFalse();
```

## Multiple logical operators in statement

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

## Nested arrow functions

```javascript
const returnFunc = () => 
  someData => (doSomeCalculation() === 1)
    ? 'RETURNED_IF_TRUE'
    : 'RETURNED_IF_FALSE';
```

## Chaining promises

```javascript
const add1ToVal = val => val + 1;
const add2ToVal = val => val + 2;

const returnPromise()
  .then(add1ToVal)
  .then(add2ToVal)
  .then(() => finalResolve());
```

## Resolving promises consecutive (without async await) 

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
