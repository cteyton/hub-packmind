<!-- #title -->
# Manage forge event delays and duplicates

<!-- #severity -->
*Warning*

<!-- #categories -->
- Atlassian Forge
- Event Management
- Best Practices

<!-- #description -->
### What
This practice is triggered when handling Forge events that may be delayed or duplicated, such as webhooks for Jira issue creation.

### Why
Managing delays and duplicates in event handling ensures that processes are not redundantly executed, which could lead to inconsistent states or unnecessary computations.

### Fix
Use a unique identifier for events and check against a storage mechanism to ensure that an event is only processed once.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
const events = require('events');

events.on("avi:jira:created:issue", async ({ payload }) => {
    console.log(`Processing issue: ${payload.issue.key}`);
    // Simulated processing logic without any checks for duplicates
    // Additional processing logic
});
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
const events = require('events');
const storage = require('some-storage-lib');

const processEvent = async ({ payload }) => {
    const issueKey = payload.issue.key;
    const alreadyProcessed = await storage.get(`issue-${issueKey}`);
    
    if (!alreadyProcessed) {
        console.log(`Processing ${issueKey}`);
        await storage.set(`issue-${issueKey}`, true);
        // Additional processing logic
    }
};

events.on("avi:jira:created:issue", async (eventData) => {
    await processEvent(eventData);
});
```
