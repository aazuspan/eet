# EET

Build and run unit tests in the [Google Earth Engine]() code editor.

## Quickstart

First, import the `eet` module:

```javascript
var eet = require("users/aazuspan/eet:eet");
```

Then write your first test using `eet.test`. This function takes a test description (to help you keep track) and a callable function to run during testing.

```javascript
eet.test("Check runMyCalculation", function() {
    var value = runMyCalculation();
    if (value != 42) throw new Error("That should have equaled 42!");
})
```

As you can see, you can write your own tests from scratch by checking conditions and throwing errors, but `eet` has an `assert` module to handle common checks. Here's the same test using the assert module.

```javascript
eet.test("Check runMyCalculation", function() {
    var value = runMyCalculation();
    eet.assert.equal(value, 42);
})
```

Once you've built all your tests, run them and display the results with `eet.run`.

```javascript
eet.run();
```

![All tests passed!](assets/eet_passed.png)

## Usage

### Tests

- test(description, function) : Register a function for testing.
- run(*pattern*) : Run tests and report the results. An optional regex pattern can be used to only run matching tests.

### Asserts

Assertions in `eet` are based on the [Node.js `assert` module](https://nodejs.org/api/assert.html) and typically follow the same format, with a couple exceptions. Note that `eet` assertions work with **client-side data only**, so use `getInfo` to compare Earth Engine objects. 

- assert.fail(*message*) : Automatically fail.
- assert.ok(value, *message*) : Value is [truthy](https://developer.mozilla.org/en-US/docs/Glossary/Truthy).
- assert.notOk(value, *message*) : Value is [falsy](https://developer.mozilla.org/en-US/docs/Glossary/Falsy).
- assert.equal(actual, expected, *message*) : Values are equal `==`.
- assert.notEqual(actual, expected, *message*) : Values are not equal `!=`.
- assert.strictEqual(actual, expected, *message*) : Values are strictly equal `===`.
- assert.strictNotEqual(actual, expected, *message*) : Values are strictly not equal `!==`.
- assert.exists(value, *message*) : Value is not `null` or `undefined`.
- assert.notExists(value, *message*) : Value is `null` or `undefined`.
- assert.match(string, regex) : String matches regex pattern.
- assert.doesNotMatch(string, regex) : String does not match regex pattern.
- assert.throws(fn, *errorLike*, *errMsgMatcher*, *message*) : Function throws error. Specify an Error-like (e.g. `ReferenceError`) to only match specific error types. Specify a regex message pattern to only match errors with a matching error message.


Every `assert` function takes an optional message as its last argument, which will override the default error message.