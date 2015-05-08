# UnitTestNOW
ServiceNow Unit Testing util for server side scripts

## UnitTestNOW Documentation

### Key Classes

1. SNUnit
2. Assertions
3. SNValidator
4. InvalidArgumentException
5. InvalidSysIDException
6. RecordNotFoundException

### SNUnit

SNUnit(setup, teardown)
Initializes the test runner object
@param  {Function} setup    A setup function
@param  {Function} teardown A teardown function

```javascript
var unit = new SNUnit();
```
The parameters are optional, as you can set them later.

setSetup(setup)
Sets the setup function
@param  {Function} setup    A setup function

```javascript
unit.setSetup(functionName);
```

setTeardown(teardown)
Sets the teardown function
@param  {Function} teardown A teardown function

```javascript
unit.setTeardown(functionName);
```

test(name, callback)
Runs a test, first calling setup, then running the passed in function, finally running the teardown
@param  {string}   name     A description of the test
@param  {Function} callback A function containing tests

```javascript
unit.test("This test does nothing", function(){
	//See, I don't do anything!
});
```

### Assertions

Assertions(tableName, functionName, testName)
Creates an assertion object
@param  {string} tableName    A table name for what is being tested
@param  {string} functionName The name of the function or class being tested
@param  {string} testName The name of the test

```javascript
var assert = new Assertions();
```

The parameters are optional, as you can set them later.

setFunctionName(functionName)
Sets the function that is being tested
@param  {string} functionName The name of the function or class being tested

```javascript
assert.setFunctionName('myFunction');
```

setTableName(tableName)
Sets the name of the table being tested
@param  {string} tableName    A table name for what is being tested

```javascript
assert.setTableName('incident');
```

setTestName(testName)
Sets the name of the test being run
@param  {string} testName The name of the test

```javascript
assert.setTestName('This is a sample test');
```

assertEqual(expected, actual, message)
Asserts that a value is equal to what is expected (==)
@param  {[type]} expected A value that is expected
@param  {[type]} actual   The actual value
@param  {string} message  A message describing the test

```javascript
assert.assertEqual('Hello', 'Hello', "Hello should equal Hello!");
```

assertDeepEqual(expected, actual, message)
Asserts that a value is equal to what is expected (===)
@param  {[type]} expected A value that is expected
@param  {[type]} actual   The actual value
@param  {string} message  A message describing the test

```javascript
assert.assertDeepEqual('Hello', 'Hello', "Hello should equal Hello!");
```

assertNotEqual(expected, actual, message)
Asserts that a value is not equal to what is expected (!=)
@param  {[type]} expected A value that is expected
@param  {[type]} actual   The actual value
@param  {string} message  A message describing the test

```javascript
assert.assertEqual('Hello', 'World', "Hello should not equal World!");
```

assertDeepNotEqual(expected, actual, message)
Asserts that a value is not equal to what is expected (!==)
@param  {[type]} expected A value that is expected
@param  {[type]} actual   The actual value
@param  {string} message  A message describing the test

```javascript
assert.assertEqual('Hello', 'World', "Hello should equal World!");
```

assertThrows(block, message)
Asserts that an exception is thrown by a function
@param  {Function} block   A block of code to execute
@param  {string} message A message describing the test

```javascript
assert.assertThrows(function(){ throw new Error();}, "My anonymous function throws an error!");
```

assertTrue(value, message)
Asserts that a value is true
@param {booleanExpression} value A boolean expression
@param {string} message A message describing the test

```javascript
assert.assertTrue(1 == 1, "One equals One");
```

assertFalse(value, message)
Asserts that a value is false
@param {booleanExpression} value A boolean expression
@param {string} message A message describing the test

```javascript
assert.assertFalse(1 == 2, "One is not equal to two");
```

pass(message)
Handles the passing of a test
@param  {string} message A message describing the test

fail(message)
Handles the failing of a test
@param  {string} message A message describing the test

cleanUpMessage(message)
Cleans up the message; returns '' if nothing was passed in
@param  {string} message A message describing the test
@return {string}         A cleaned up message

createResultRecord(message, flag)
Logs the result to a table in ServiceNow
@param  {string} message A message describing the test
@param  {boolean} flag    Whether or not the test passed

### SNValidator

SNValidator()
Creates a new validator object

```javascript
var validator = new SNValidator();
```

checkValidStringArgument(string)
Validates that an argument is, in fact, a string
@param  {string} string A string to test
@return {boolean}        true if an object

```javascript
validator.checkValidStringArgument('what'); //true
validator.checkValidStringArgument({}); //false
```

checkValidObjectArgument(object)
Validates that an argument is, in fact, an object
@param  {Object} object An object to test
@return {Boolean}        true if an object

```javascript
validator.checkValidObjectArgument({}); //true
validator.checkValidObjectArgument(2); //false
```

checkValidNumberArgumentLoose(number)
Validates than an argument is, in fact, a valid number, but uses == instead of ===
@param  {number} number A number to test
@return {boolean}        true if the value is a number

```javascript
validator.checkValidNumberArgumentLoose(1); //true
validator.checkValidNumberArgumentLoose('1'); //true
validator.checkValidNumberArgumentLoose('Potatoes'); //false
```


checkValidNumberArgumentStrict(number)
Validates than an argument is, in fact, a valid number, but uses === instead of ==
@param  {number} number A number to test
@return {boolean}        true if the value is a number

```javascript
validator.checkValidNumberArgumentStrict(1); //true
validator.checkValidNumberArgumentStrict('1'); //false
```

checkValidSysIDArgument(sys_id)
Validates that an argument is, in fact, a sys_id
@param  {string} sys_id A string to test
@return {Boolean}        true if a sys_id

```javascript
validator.checkValidSysIDArgument('153ebc53a4377100764f456eb40d41f1'); //true
validator.checkValidSysIDArgument('peasAndCarrots!'); //false
```

checkValidCallbackArgument(callback)
Validates that an argument is, in fact, a function to callback
@param  {Function} callback     A function to test
@return {boolean}                true if a valid function (or object)

```javascript
validator.checkValidCallbackArgument(function(){}); //true
validator.checkValidCallbackArgument({}); //false
```

### InvalidArgumentException

InvalidArgumentException(argument, functionName)

```javascript
throw new InvalidArgumentException('potatoes', 'myFunction');
```

### InvalidSysIDException

InvalidSysIDException(sys_id, functionName)

```javascript
throw new InvalidSysIDException('bananas', 'myOtherFunction');
```

### RecordNotFoundException

RecordNotFoundException(table, functionName)

```javascript
throw new RecordNotFoundException('incident', 'myIncidentFinder');
```
