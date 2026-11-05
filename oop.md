# 1. Object-Oriented Programming (OOP)

## 1.1 What is OOP?

Object-Oriented Programming is a programming paradigm that organizes code around objects and classes.

It helps make software:

- Reusable
- Maintainable
- Modular
- Easier to extend

Example: In an employee management system, an Employee can be represented as an object with properties and methods.

### Class vs Object

| Class                          | Object                 |
| ------------------------------ | ---------------------- |
| Blueprint/template             | Instance of a class    |
| Defines properties and methods | Contains actual values |
| Logical definition             | Runtime entity         |

```
class Employee {
    constructor(name, salary) {
        this.name = name;
        this.salary = salary;
    }

    getDetails() {
        return this.name;
    }
}

const emp1 = new Employee("Nova", 40000);
```

Here:

- `Employee` = Class
- `emp1` = Object
- `name`, `salary` = Properties
- `getDetails()` = Method
- `constructor()` = Initializes an object.

## 1.2 Four pillars of OOP

These are extremely important for interviews.

1\. Encapsulation

Data hiding and controlled access

2\. Inheritance

Code reusability

3\. Polymorphism

One interface, multiple behaviours

4\. Abstraction

Hiding implementation details

### A. Encapsulation

Definition: Wrapping data (properties) and methods into a single unit (class) and restricting direct access to internal data.

Example: A bank account should not allow anyone to directly change its balance.

```
class BankAccount {
    #balance = 1000;

    deposit(amount) {
        if (amount > 0) {
            this.#balance += amount;
        }
    }

    getBalance() {
        return this.#balance;
    }
}
```

Here:

- `#balance` is private.
- It cannot be accessed directly outside the class.
- Balance changes through controlled methods.

Real-life example: ATM allows you to withdraw money through controlled operations rather than directly modifying your bank balance.

Why is encapsulation useful?

- Data protection
- Controlled modification
- Validation
- Reduced unintended changes

### B. Inheritance

Definition: A class acquires properties and methods from another class.

It promotes code reusability.

```
class User {
    login() {
        return "User logged in";
    }
}

class Admin extends User {
    deleteUser() {
        return "User deleted";
    }
}

const admin = new Admin();

admin.login();
admin.deleteUser();
```

Here:

- `User` = Parent/Base class
- `Admin` = Child/Derived class
- `extends` = Inheritance keyword.

Types of inheritance

| Type         | Meaning                          |
| ------------ | -------------------------------- |
| Single       | One parent → one child           |
| Multilevel   | Grandparent → Parent → Child     |
| Hierarchical | One parent → multiple children   |
| Multiple     | One child → multiple parents     |
| Hybrid       | Combination of inheritance types |

[Inheritance in Java | Java Tutorial | PrepInsta](https://images.openai.com/static-rsc-4/pO8ozk0At_2xbp-uSRUbc0RhoKuj0aNF7Y9qQrqKo5OtGmAd5voEbfhL8KWMu84hdx91U1wnVBCUnqdh8pus57_7ZvNe0CMm2Sn3iDJ2b599LCN30kibBIlRg4jLaJR9vBvLN1KCF4le6_SIOHQxrUNZlp3ZnPaaTzTcI0nG_jE?purpose=inline)

[prepinsta.com](https://prepinsta.com/java/inheritance/?utm_source=chatgpt.com)

Important: JavaScript classes support single class inheritance. Python supports multiple inheritance. Java does not support multiple inheritance through classes, but supports multiple interfaces.

Backend scenario: Admin, Customer and Seller can inherit common functionality from a User class.

### C. Polymorphism

Definition: Polymorphism means one interface or method name can have different behaviours depending on the object or context.

Two major types:

1\. Compile-time polymorphism

Generally achieved through method overloading or operator overloading.

Example of method overloading in Java:

```
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}
```

2\. Runtime polymorphism

Achieved through method overriding.

```
class Animal {
    sound() {
        return "Animal sound";
    }
}

class Dog extends Animal {
    sound() {
        return "Bark";
    }
}

class Cat extends Animal {
    sound() {
        return "Meow";
    }
}
```

The same method `sound()` behaves differently depending on the object.

Backend scenario: Different payment methods can implement the same `pay()` method differently.

- UPI payment
- Credit card payment
- Net banking payment

Important interview distinction:

| Overloading                            | Overriding                                            |
| -------------------------------------- | ----------------------------------------------------- |
| Same method name, different parameters | Child redefines inherited method                      |
| Usually compile-time                   | Runtime                                               |
| Different parameter lists              | Same method signature (in conventional OOP languages) |
| Java supports it                       | Java and JavaScript support overriding                |

JavaScript does not have traditional method overloading based on parameter signatures. A later method definition replaces an earlier one.

### D. Abstraction

Definition: Hiding implementation details and exposing only essential functionality.

Example:

```
class Payment {
    pay(amount) {
        throw new Error("Implement in subclass");
    }
}

class UPIPayment extends Payment {
    pay(amount) {
        return `Paid ${amount} using UPI`;
    }
}
```

The user only needs to call `pay()`. The internal payment processing is hidden.

Real-life example: When you drive a car, you use the steering wheel and pedals without needing to understand the internal engine mechanism.

Backend scenario: A payment API exposes an endpoint to initiate payment. The client doesn't need to know the internal payment gateway implementation.

### Encapsulation vs Abstraction

This is a common interview question.

| Encapsulation                                          | Abstraction                                               |
| ------------------------------------------------------ | --------------------------------------------------------- |
| Protects internal data                                 | Hides implementation complexity                           |
| Focuses on access control                              | Focuses on essential behaviour                            |
| Achieved using access modifiers and controlled methods | Achieved using interfaces, abstract classes and contracts |

Remember:

- Encapsulation = How to protect data?
- Abstraction = What to expose and what to hide?

## 1.3 Important OOP concepts beyond four pillars

| Concept          | Meaning                                                      |
| ---------------- | ------------------------------------------------------------ |
| Constructor      | Initializes an object                                        |
| Destructor       | Handles object cleanup in languages that support destructors |
| `this`           | Refers to the current object/context                         |
| `super`          | Accesses parent-class functionality                          |
| Static method    | Belongs to the class, not an individual instance             |
| Instance method  | Operates on an object                                        |
| Access modifiers | Control accessibility                                        |
| Interface        | Defines a contract                                           |
| Abstract class   | Provides a partially implemented base class                  |
| Composition      | Builds a class using objects of other classes                |

### Access modifiers

| Modifier  | Accessibility                                                                |
| --------- | ---------------------------------------------------------------------------- |
| Public    | Accessible from anywhere                                                     |
| Private   | Accessible within the class                                                  |
| Protected | Accessible within the class and derived classes, depending on language rules |

Note: JavaScript has `#private` fields and methods. Its `protected` access modifier is not a native JavaScript class feature.

### Abstract class vs Interface

| Abstract class                       | Interface                                        |
| ------------------------------------ | ------------------------------------------------ |
| Can contain implemented methods      | Defines a contract (language-dependent features) |
| Can contain state                    | Usually describes required structure/behaviour   |
| Can have constructors                | Cannot be instantiated                           |
| Java class can extend only one class | Java class can implement multiple interfaces     |

Python uses the `abc` module for abstract base classes. JavaScript has no native `interface` keyword.

## 1.4 Composition vs Inheritance

Inheritance: IS-A relationship.

Example: Dog IS-A Animal.

Composition: HAS-A relationship.

Example: Car HAS-A Engine.

Composition often provides better flexibility when building complex backend systems because components can be replaced independently.

## 1.5 Practical backend OOP scenario

Imagine an e-commerce application.

- `User` – common user functionality.
- `Customer` – customer-specific operations.
- `Admin` – administrative operations.
- `Payment` – common payment interface.
- `UPIPayment` – UPI implementation.
- `CardPayment` – card implementation.

Which concepts are used?

| Scenario                          | OOP concept   |
| --------------------------------- | ------------- |
| Admin inherits User               | Inheritance   |
| Private user password field       | Encapsulation |
| Different payment implementations | Polymorphism  |
| Exposing payment interface        | Abstraction   |

## 1.6 Tricky OOP MCQ facts

1. Constructor is generally not inherited as a normal method.
2. A class is a blueprint; an object is an instance.
3. Static methods belong to the class rather than individual objects.
4. Method overriding enables runtime polymorphism.
5. Private members are not directly accessible outside their class.
6. Java supports multiple inheritance through interfaces, not classes.
7. Python supports multiple inheritance.
8. JavaScript uses prototype-based inheritance.
9. Composition represents a HAS-A relationship.
10. Encapsulation and abstraction are related but not identical.