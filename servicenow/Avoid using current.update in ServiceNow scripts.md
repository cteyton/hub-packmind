<!-- #title -->
# Avoid using current.update in ServiceNow scripts

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Performance
- Best Practices

<!-- #description -->
### What
The practice involves avoiding unnecessary or repeated calls to the current.update() function within ServiceNow scripts, especially when it may trigger associated recursive Business Rules.

### Why
Unnecessary calls to current.update() can lead to performance issues due to recursive calls to Business Rules, which, although detected by the system's internal mechanisms, can still degrade the performance of an instance.

### Fix
To comply with this rule, avoid using the current.update() function unless it is essential, and consider alternative methods to achieve the desired result without triggering recursive Business Rules.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// Bad Practice
// Using current.update unnecessarily
current.some_field = new_value;
current.update();  // This may trigger unnecessary Business Rules, leading to performance issues
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// Good Practice
// Perform necessary updates directly to fields without calling current.update()
if (current.some_field != new_value) {
    current.some_field = new_value;
    // Avoid calling current.update() to prevent triggering unnecessary Business Rules
}
```
