# Javascript Code Smells

### Introduction
*In computer programming, code smell is any symptom in the source code of a program that possibly indicates a deeper problem. According to Fowler, "a code smell is a surface indication that usually corresponds to a deeper problem in the system"* - [Code Smell - Wikipedia](https://en.wikipedia.org/wiki/Code_smell)

Bottom line, we need to refactor code with smells to make it more maintainable and reduce the number of bugs it introduces.

### Table of Contents
  1. [Purposeless conditions](#purposeless-conditions)
  2. [Multiple return statements](#redundant-returns)
  
## Purposeless conditions

#### Synopsis
Purposeless conditions introduce unwanted complexity to the code. It also increases the vertical length of the function subtracting the readablity.

**Avoid**
```javascript
  /* Example # 1 */
  function isNumber(test){
    if(typeof test === 'number')
      return true;
    else
      return false;
  }

  /* Example # 2 */
  function isNotBoolean(test){
    var retVal = false; //or any other initialization
    if(typeof test === 'boolean'){
      retVal = false;
    }
    else{
      retVal = true;
    }
    return retVal;
  }
```
**Score**
```javascript
  /* Example # 1*/
  function isNumber(test){
    return typeof test === 'number';
  }
  
  /* Example #2 */
  function isNotBoolean(test){
    return typeof test !== 'boolean';
  }
```

## Multiple return statements

#### Synopsis
There should generally be a single returning path from a function. Multiple `return` statements make it difficult to understand the flow of the function.

**Avoid**
```javascript
  /* Example */
  function stringAdd(numString){
    var val = parseInt(numString);
    if(numString === NaN){
      return 0;
    }
    else{
      return val;
    }
  }
```

**Score**
```javascript
  /* Example */
  function stringAdd(numString){
    var val = parseInt(numString);
    return val === NaN ? 0 : val;
  }
```
### Contribution
Send in your PRs in the following pattern:
- Let there be a pattern
