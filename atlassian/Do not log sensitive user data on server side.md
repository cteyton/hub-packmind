<!-- #title -->
# Do not log sensitive user data on server side

<!-- #severity -->
*Warning*

<!-- #categories -->
- Forge

<!-- #description -->
### What is it?
This practice is triggered when code logs information obtained from user input and includes any sensitive data such as passwords, financial details, or personally identifiable information that should remain confidential.

### Why apply it?
Logging sensitive user data can lead to security breaches and compliance issues, as attackers or unauthorized parties might access logs to gather personal data, creating severe privacy risks.

### How to Fix it?
Ensure that any logging mechanism excludes or masks sensitive elements by sanitizing, redacting, or encrypting the data before logging.



<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
import Resolver from '@forge/resolver';
import api, { route } from "@forge/api";

export const fetchUserEmail = async () => {
  const response = await api.asUser().requestJira(route`/rest/api/3/myself`);
  const userData = await response.json();

  console.info(`User Email Retrieved: ${userData.emailAddress}`); // ✅ Logs securely on server

  return userData.emailAddress; // Returns the email
};

const resolver = new Resolver();

resolver.define('getText', (req) => {
  console.log(req);
  return 'Hello, world!';
});

export const handler = resolver.getDefinitions();

```

## Example 2:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
import Resolver from '@forge/resolver';
import api, { route } from "@forge/api";

export const fetchUserEmail = async () => {
  const response = await api.asUser().requestJira(route`/rest/api/3/myself`);
  const user = await response.json();

  logger.info(`User Email Retrieved: ${user.emailAddress}`);

  return userData.emailAddress; // Returns the email
};

const resolver = new Resolver();

resolver.define('getText', (req) => {
  console.log(req);
  return 'Hello, world!';
});

export const handler = resolver.getDefinitions();

```
