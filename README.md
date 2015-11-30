# Javascript Code Smells

### Introduction
*In computer programming, code smell is any symptom in the source code of a program that possibly indicates a deeper problem. According to Fowler, "a code smell is a surface indication that usually corresponds to a deeper problem in the system"* - [Code Smell - Wikipedia](https://en.wikipedia.org/wiki/Code_smell)

Bottom line, we need to refactor code with smells to make it more maintainable and reduce the number of bugs it introduces.

### Table of Contents
  1. [Purposeless conditions](#purposeless-conditions)
  2. [Multiple return statements](#redundant-returns)
  3. [This or That](#this-or-that)
  4. [Equality](#equality)
  
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

## This or That

#### Synopsis
Assigning `this` to a variable is a general practive to maintain context in a function. This works but stinks and makes the code less recognizeable. Using constructs `bind`, `call` and `apply` to set context while calling a function is a more cleaner approach. Functions like `forEach` have a hidden parameter to set execution context.

**Avoid**
```javascript
  /* Example 1*/
  function haircut(persons){
    var that = this;
    
    persons.forEach(function(person){
      that.cut(person);
    });
  }
```

**Score**
```javascript
  /* Example 1*/
  function haircut(persons){
    persons.forEach(function(person){
      this.cut(person);
    }.bind(this));
  }
  
  /* Example 1 Alternate*/
  function haircut(persons){
    persons.forEach(function(person){
      this.cut(person);
    }, this); //hidden param to set context in `forEach`
  }
```

## Equality

#### Synopsis
Javascript has two options when it comes to comparing values the double equals `==` and the triple equals `===` operators. The difference between the two is that triple equals does type checking as well as value checking, so `1 === '1'` would be false where as `1 == '1'` would be true. In order to avoid nasty surprises we should try to use the `===` majority of the time since it helps us assert the types as well.

**Avoid**
```javascript
  /* Example */
  function isSomeNumString(numString){
    return numString == 5;
  }
```

**Score**
```javascript
  /* Example */
  function isSomeNumString(numString){
    return numString === '5';
  }
```

### Contribution
Send in your PRs in the following pattern:
- Let there be a pattern
