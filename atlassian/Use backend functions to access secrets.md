<!-- #title -->
# Use backend functions to access secrets

<!-- #severity -->
*Warning*

<!-- #categories -->
- Security
- Javascript
- Serverless

<!-- #description -->
### What
Attempting to access secrets directly from the UI Kit or frontend will result in errors as secrets only function in the backend.

### Why
Accessing secrets from the frontend can lead to security vulnerabilities as sensitive information may be exposed to client-side users.

### Fix
Create a backend function to retrieve secrets securely and call this function from the frontend using an API or method invocation.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// Attempting to access secrets directly in frontend code
import { secrets } from '@forge/secrets';

async function fetchApiKey() {
    const apiKey = await secrets.get("apiKey"); // ❌ Problème
    console.log(apiKey);
}

fetchApiKey();
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// Backend function to securely access secrets
export async function getSecret() {
    return await secrets.get("apiKey");
}

// Frontend code using invoke to call the backend function
import { invoke } from '@forge/ui';

async function fetchApiKey() {
    const apiKey = await invoke('getSecret', {});
    console.log(apiKey); // Securely obtained API key
}

fetchApiKey();
```
