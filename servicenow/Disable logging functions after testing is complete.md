<!-- #title -->
# Disable logging functions after testing is complete

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Logging
- Performance

<!-- #description -->
### What
Logging functions like gs.log() and gs.info() should be disabled in production code after they have served their purpose during development and testing.

### Why
Leaving logging functions enabled after testing can lead to unnecessary log file entries, which can clutter logs and affect system performance due to increased log file size.

### Fix
Review the code after testing is complete and remove or comment out any gs.log() and gs.info() function calls that are no longer necessary.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
function myFunction() {
  // Code logic here

  // Logging is active in production code
  gs.log('Function executed successfully.');
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
function myFunction() {
  // Code logic here
  
  // Commenting out logging after testing.
  // gs.log('Function executed successfully.');
}
// Keep logging disabled in production.
```
