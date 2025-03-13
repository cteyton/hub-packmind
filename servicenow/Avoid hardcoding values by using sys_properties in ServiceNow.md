<!-- #title -->
# Avoid hardcoding values by using sys_properties in ServiceNow

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Best Practices
- Maintainability

<!-- #description -->
### What
Hardcoding values directly in ServiceNow scripts can create maintenance challenges and reduce flexibility, as these values are not easily adjustable or reusable across different scripts.

### Why
Using hardcoded values reduces the code quality and makes it difficult to update values uniformly across multiple scripts, leading to potential inconsistencies or errors when values need adjustment.

### Fix
Store the values in sys_properties and access them using gs.getProperty(), which allows for centralized value management and easier updates.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// Hardcoded threshold value
var threshold = 100;

if (current.value > threshold) {
    gs.info("The value exceeds the threshold.");
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// Retrieve property value using sys_properties
var threshold = gs.getProperty('com.mycompany.threshold');

if (current.value > threshold) {
    gs.info("The value exceeds the threshold.");
}
```
