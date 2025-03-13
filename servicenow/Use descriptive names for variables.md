<!-- #title -->
# Use descriptive names for variables

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Best Practices
- Code Readability

<!-- #description -->
### What
Variable names should clearly communicate the purpose and function of the variable, avoiding generic names like 'gr'.

### Why
Descriptive variable names improve code readability and maintainability, allowing developers to understand the code's functionality without requiring extensive comments or documentation.

### Fix
Replace generic or unclear variable names with names that accurately describe the variable's use or purpose.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
var gr = current.getUserDetails();
var x = etc.getIncidents();
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
var userRecord = current.getUserDetails();
var incidentList = etc.getIncidents();
```
