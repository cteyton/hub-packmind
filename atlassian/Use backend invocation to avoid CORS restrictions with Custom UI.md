<!-- #title -->
# Use backend invocation to avoid CORS restrictions with Custom UI

<!-- #severity -->
*Warning*

<!-- #categories -->
- Javascript
- CORS
- API

<!-- #description -->
### What
This practice is applicable when making requests to Jira APIs from a Custom UI using React or Vue, where direct requests result in CORS issues.

### Why
CORS restrictions prevent direct API requests from the frontend for security reasons, making it necessary to use server-side invocations to access Jira APIs.

### Fix
To adhere to this practice, migrate API requests to be made from the backend by defining a function that uses `api.asUser()` or `api.asApp()`, and invoke this backend function from the frontend.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// Directly from the frontend
const response = await fetch("https://your-instance.atlassian.net/rest/api/3/issue/TEST-123");
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// Frontend
const issue = await invoke("getIssue", { issueKey: "TEST-123" });

// Backend
export async function getIssue({ issueKey }) {
  const response = await api.asApp().requestJira(`/rest/api/3/issue/${issueKey}`);
  return response.json();
}
```
