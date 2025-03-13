<!-- #title -->
# Use GlideAjax for server interactions in client scripts

<!-- #severity -->
*Warning*

<!-- #categories -->
- ServiceNow
- Javascript
- Security

<!-- #description -->
# ### What
This practice is triggered when implementing interactions between client scripts and server-side scripts in ServiceNow.

### Why
Directly embedding server-side code into client scripts can lead to significant security risks and maintenance challenges in a ServiceNow environment.

### Fix
Use ServiceNow's GlideAjax() to perform asynchronous server calls from client scripts, allowing secure and maintainable server interactions.


<!-- #examples -->

## Example 1:

<!-- #example-->

### Negative

<!-- #example_negative_code-->

```js
function getServerDataDirectly() {
  // Directly embedding server-side script code into client script
  eval("var records = new GlideRecord('incident'); records.query(); while(records.next()){ gs.print(records.number); }");
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_code-->

```js
function getServerData() {
  var ga = new GlideAjax('MyScriptInclude');
  ga.addParam('sysparm_name', 'getData');
  ga.getXMLAnswer(handleResponse);
}

function handleResponse(response) {
  var serverData = response;
  console.log(serverData);
}
```
