<!-- #title -->
# Conditionals Should Start on New Lines

<!-- #severity -->
*Critical*

<!-- #categories -->
- readability
- maintainability

<!-- #description -->
## What is it?
This practice requires that each conditional statement (such as `if`, `else if`, or `else`) starts on its own new line. Writing a new conditional on the same line as a closing `}` from a previous block can confuse the reader and indicate that the statements might be unintentionally related.

## Why apply it?
Having conditionals on the same line as a closing brace can obscure the logical separation between distinct blocks of code. This ambiguity can lead to misunderstandings about the program’s flow and increase the risk of introducing bugs. Keeping each conditional on its own line improves the clarity and maintainability of your code.

## How to Fix it?
Always begin a new conditional statement on a new line. If the conditions are related, consider using constructs like `else if` on separate lines. Ensure that each block is clearly delimited to enhance readability.

<!-- #examples -->

## Example 1:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
In this positive example, each conditional starts on a new line, clearly separating independent checks.

<!-- #example_positive_code-->
```ts
if (user.isActive) {
  console.log("User is active");
}

if (user.isAdmin) {
  console.log("User is admin");
}

if (!user.hasProfile) {
  console.log("User does not have a profile");
}
```

### Negative

<!-- #example_negative_description-->
In this negative example, the second `if` begins immediately after the closing `}` of the first block on the same line, potentially leading to misinterpretation of the intended control flow.

<!-- #example_negative_code-->
```ts
if (user.isActive) {
  console.log("User is active");
} if (user.isAdmin) {  /* Noncompliant */
  console.log("User is admin");
} if (!user.hasProfile) {
  console.log("User does not have a profile");
}
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
In this positive example, a chain of related conditions is clearly formatted with each `else if` and `else` correctly starting on a new line.

<!-- #example_positive_code-->
```ts
if (temperature < 0) {
  console.log("Freezing");
} else if (temperature < 20) {
  console.log("Cold");
} else if (temperature < 30) {
  console.log("Warm");
} else {
  console.log("Hot");
}
```

### Negative

<!-- #example_negative_description-->
Even though `else if` is used in this negative example, the conditional following a closing brace is incorrectly placed on the same line, which reduces clarity.

<!-- #example_negative_code-->
```ts
if (temperature < 0) {
  console.log("Freezing");
} else if (temperature < 20) {  /* Noncompliant: should start on a new line */
  console.log("Cold");
} else if (temperature < 30) {
  console.log("Warm");
} else {
  console.log("Hot");
}
```

## Example 3:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
In this positive example, different status checks are separated by new lines, ensuring that each condition is immediately apparent and isolated from the others.

<!-- #example_positive_code-->
```ts
if (data.status === "loading") {
  displayLoader();
}

if (data.status === "error") {
  handleError(data.error);
}

if (data.status === "success") {
  processData(data.payload);
}
```

### Negative

<!-- #example_negative_description-->
In this negative example, the condition for an error status appears on the same line as the closing bracket of the previous check, which may lead to an incorrect association between the blocks.

<!-- #example_negative_code-->
```ts
if (data.status === "loading") {
  displayLoader();
} if (data.status === "error") {  /* Noncompliant */
  handleError(data.error);
} if (data.status === "success") {
  processData(data.payload);
}
```