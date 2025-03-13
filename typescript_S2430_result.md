<!-- #title -->
# Constructors Should Start with an Uppercase Letter

<!-- #severity -->
*Critical*

<!-- #categories -->
- reliability
- readability

<!-- #description -->
## What is it?
This practice enforces that constructor function names must begin with an uppercase letter. This naming convention acts as a reminder that a constructor function is meant to be invoked with the new keyword and distinguishes it from regular functions.

## Why apply it?
Using a lowercase name for a constructor can lead to accidental calls of the function without the new keyword, which may result in unexpected behavior. Following this naming convention improves code clarity and reduces potential errors.

## How to Fix it?
Ensure that the name of any function intended to be used as a constructor starts with an uppercase letter. Rename any misnamed constructor functions to clearly indicate their purpose and encourage proper instantiation using the new keyword.

<!-- #examples -->

## Example 1:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
The positive example correctly defines a constructor function with an uppercase name. In this example, the constructor sets object properties and provides a method to format the full name.

<!-- #example_positive_code-->

```ts
function Person(firstName: string, middleInitial: string, lastName: string) {
  this.firstName = firstName;
  this.middleInitial = middleInitial;
  this.lastName = lastName;
  this.getFullName = function(): string {
    return `${this.firstName} ${this.middleInitial}. ${this.lastName}`;
  };
}

const personInstance = new Person("John", "H", "Doe");
console.log(personInstance.getFullName());
```

### Negative

<!-- #example_negative_description-->
The negative example uses a lowercase name for the constructor function. This may lead to calling the function without the new keyword, causing properties to be set on the global object (or resulting in an error in strict mode).

<!-- #example_negative_code-->

```ts
function person(firstName: string, middleInitial: string, lastName: string) {
  this.firstName = firstName;
  this.middleInitial = middleInitial;
  this.lastName = lastName;
  this.getFullName = function(): string {
    return this.firstName + " " + this.middleInitial + ". " + this.lastName;
  };
}

const personInstance = person("Jane", "A", "Smith"); // Noncompliant: missing 'new'
console.log(personInstance);
```

## Example 2:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
This compliant example demonstrates a class-based constructor with an uppercase name and proper type annotations, ensuring clear instantiation and method definition.

<!-- #example_positive_code-->

```ts
class Employee {
  employeeId: number;
  name: string;
  position: string;

  constructor(employeeId: number, name: string, position: string) {
    this.employeeId = employeeId;
    this.name = name;
    this.position = position;
  }

  getEmployeeDetails(): string {
    return `ID: ${this.employeeId}, Name: ${this.name}, Position: ${this.position}`;
  }
}

const emp = new Employee(123, "Alice", "Engineer");
console.log(emp.getEmployeeDetails());
```

### Negative

<!-- #example_negative_description-->
The negative example defines a constructor-like function using a lowercase name instead of using the class syntax. This may mislead developers into invoking the function without the new keyword, potentially leading to runtime errors.

<!-- #example_negative_code-->

```ts
function employee(employeeId: number, name: string, position: string) {
  this.employeeId = employeeId;
  this.name = name;
  this.position = position;
  this.getEmployeeDetails = function(): string {
    return "ID: " + this.employeeId + ", Name: " + this.name + ", Position: " + this.position;
  };
}

const emp = employee(456, "Bob", "Manager"); // Noncompliant: missing 'new'
console.log(emp ? emp.getEmployeeDetails() : "No employee created");
```

## Example 3:

<!-- #example-->

### Positive

<!-- #example_positive_description-->
In this compliant example, a constructor function within a namespace uses an uppercase name, clearly indicating its intent to be used with the new keyword. It also includes a method to compute a value based on the object's properties.

<!-- #example_positive_code-->

```ts
namespace Models {
  export function Product(name: string, price: number, category: string) {
    this.name = name;
    this.price = price;
    this.category = category;
    this.getPriceWithTax = function(taxRate: number): number {
      return this.price * (1 + taxRate);
    };
  }
}

const productInstance = new (Models as any).Product("Laptop", 1200, "Electronics");
console.log(productInstance.getPriceWithTax(0.15));
```

### Negative

<!-- #example_negative_description-->
This negative example incorrectly defines a constructor function within a namespace using a lowercase name. The improper naming increases the risk of it being misused without the new keyword, leading to unintended side effects.

<!-- #example_negative_code-->

```ts
namespace Models {
  export function product(name: string, price: number, category: string) {
    this.name = name;
    this.price = price;
    this.category = category;
    this.getPriceWithTax = function(taxRate: number): number {
      return this.price * (1 + taxRate);
    };
  }
}

const productInstance = (Models as any).product("Smartphone", 800, "Electronics"); // Noncompliant
console.log(productInstance ? productInstance.getPriceWithTax(0.2) : "No product created");
```