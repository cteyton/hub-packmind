<!-- #title -->
# Disable cache for requests with dynamic data

<!-- #severity -->
*Warning*

<!-- #categories -->
- Javascript
- API
- Performance

<!-- #description -->
# ### What
When interacting with APIs, especially when fetching data that may change frequently, cached responses can lead to outdated information being used.

### Why
Caching can cause inconsistencies when the server's data changes, and this may lead to displaying incorrect or stale information to users.

### Fix
Disable caching for HTTP requests when retrieving data that is subject to frequent change to ensure fresh data is always returned.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
const response = await api.asApp().requestJira(`/rest/api/3/issue/TEST-123`);
if (response.ok) {
    const issueData = await response.json();
    console.log('Issue retrieved:', issueData);
} else {
    console.error('Failed to retrieve issue:', response.status, response.statusText);
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
const response = await api.asApp().requestJira(`/rest/api/3/issue/TEST-123`, {
    headers: { 
        "Cache-Control": "no-cache",
        "Pragma": "no-cache"
    }
});
if (response.ok) {
    const issueData = await response.json();
    console.log('Issue retrieved:', issueData);
} else {
    console.error('Failed to retrieve issue:', response.status, response.statusText);
}
```
