<!-- #title -->
# Encapsulate reusable logic in script includes or functions

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Code Reusability
- Modularity

<!-- #description -->
### What
Directly performing operations within scripts without encapsulating them in reusable functions or script includes can lead to code duplication and reduce readability.

### Why
Encapsulating logic encourages the reuse and modularization of code, making it easier to maintain, test, and update, reducing the risk of errors and inefficiencies.

### Fix
Identify repetitive or complex logic and encapsulate it in standalone functions or script includes, thereby allowing multiple scripts to utilize the same code without duplicating it.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// Direct logic without encapsulation
var threshold = gs.getProperty('com.mycompany.threshold');
if (current.value > threshold) {
    gs.info("The value exceeds the threshold.");
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// Script include example
var MyScriptIncludes = Class.create();
MyScriptIncludes.prototype = {
    initialize: function() {},

    calculateThreshold: function(value) {
        var threshold = gs.getProperty('com.mycompany.threshold');
        return value > threshold;
    }
};

// Usage in script
var myScripts = new MyScriptIncludes();
if (myScripts.calculateThreshold(current.value)) {
    gs.info("The value exceeds the threshold.");
}
```
