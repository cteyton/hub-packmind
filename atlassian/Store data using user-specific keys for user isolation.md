<!-- #title -->
# Store data using user-specific keys for user isolation

<!-- #severity -->
*Warning*

<!-- #categories -->
- Atlassian Forge
- Javascript
- Storage

<!-- #description -->
# ### What
This practice is triggered when using global storage without differentiating data between users, which can be identified by code that uses generic keys like "theme" without reference to a unique user identifier. Violating code typically stores values in storage using fixed keys that can be accessed by any user.

### Why
This rule matters because using global storage can cause data leakage across users, leading to privacy issues and unpredictable application behavior. Enforcing this practice ensures that each user's data remains isolated, secure, and contextually relevant.

### Fix
To fix the issue, append a unique identifier, such as context.accountId, to the storage key when setting and retrieving data. This change ensures that the stored data is isolated per user, preventing unauthorized access between users.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
// bad practice: using a global key that is shared among all users in Atlassian Forge
async function setTheme(themeValue) {
  // Sets a generic theme key that does not differentiate between users
  await storage.set("theme", themeValue);
  console.log(`Theme set to ${themeValue} for all users`);
  
  // Retrieving the theme without user context
  const storedTheme = await storage.get("theme");
  console.log(`Retrieved theme: ${storedTheme}`);
  
  // Any additional logic relying on this value might leak user preferences
  if (storedTheme === "dark") {
    console.log("Dark theme applied globally, exposing user-specific settings...");
  }
}

// Example call without differentiating user identity
setTheme("dark");
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
// good practice: storing data using user-specific keys in Atlassian Forge
async function setUserTheme(context, themeValue) {
  // Derive a unique key per user using the user's accountId
  const userKey = context.accountId;
  const storageKey = `theme-${userKey}`;
  
  // Set the theme for the specific user
  await storage.set(storageKey, themeValue);
  console.log(`Theme set to ${themeValue} for user ${userKey}`);
  
  // Later, retrieve the user's theme setting
  const storedTheme = await storage.get(storageKey);
  console.log(`Retrieved theme for user ${userKey}: ${storedTheme}`);
  
  // Additional logic can be added based on user-specific settings
  if (storedTheme === "dark") {
    // Apply dark theme configurations
    console.log("Applying dark theme configurations...");
  }
}

// Example usage with a simulated context
const context = { accountId: "user-1234" };
setUserTheme(context, "dark");
```
