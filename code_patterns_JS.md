```javascript
return (doSomeCalculation() === 1) 
  ? doWhenTrue()
  : doWhenFalse();
```
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
```javascript
const returnFunc = () => 
  someData => (doSomeCalculation() === 1)
    ? 'RETURNED_IF_TRUE'
    : 'RETURNED_IF_FALSE';
 ```
