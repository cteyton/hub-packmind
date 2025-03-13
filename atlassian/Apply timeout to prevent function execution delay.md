<!-- #title -->
# Apply timeout to prevent function execution delay

<!-- #severity -->
*Warning*

<!-- #categories -->
- Javascript
- Performance
- Serverless

<!-- #description -->
# ### What
Functions in Forge environments are terminated if their execution exceeds 25 seconds, which can occur when waiting for a slow API response.

### Why
Enforcing this practice ensures that functions do not exceed the maximum allowed execution time, preventing unexpected terminations and potential functional failures.

### Fix
Implementing a timeout mechanism or breaking down the process into multiple steps will help manage execution time within limits.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
export async function myLongTask() {
    const response = await fetch("https://slow-api.com/data");
    return await response.json(); // May timeout if the API response takes longer than 25 seconds
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
const controller = new AbortController();
const timeout = setTimeout(() => controller.abort(), 20000); // Timeout after 20s

export async function fetchData() {
    const response = await fetch("https://slow-api.com/data", { signal: controller.signal });
    clearTimeout(timeout);
    return response.json();
}
```
