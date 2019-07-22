# Class

## Public, private, and protected modifiers

### Public

```ts
class Animal {
    name: string; // both are same
    public legs : string; //
}
```

### Private

ex-1

```ts
class Animal {
    private name: string; // both are same
    constructor(name){this.name = name}
}
console.log(new Animal("Rhino").name) // throws error as name is private
```

ex-2

```ts
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

class Rhino extends Animal {
    constructor() { super("Rhino"); }
}

class Employee {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}

let animal = new Animal("Goat");
let rhino = new Rhino();
let employee = new Employee("Bob"); 

animal = rhino;
animal = employee; // Error: 'Animal' and 'Employee' are not compatible// Error: 'Animal' and 'Employee' are not compatible
```

### Protected

The `protected` modifier acts much like the private modifier with the exception that members declared `protected can also be accessed within deriving classes.`

```ts
class Person {
    protected name: string;
    constructor(name: string) { this.name = name; }
}

class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }

    public getElevatorPitch() {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}

let howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); // error
```

### Protected constructor

If constructor of a class is prtected then the class cannot have any instances, but derived classes can have

```ts
class Person {
    protected name: string;
    protected constructor(name: string) { this.name = name; }
}
class Employee extends Person {
    private department: string;

    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }
}
let howard = new Employee("Howard", "Sales");
let john = new Person("John"); // Error: The 'Person' constructor is protected
```

## Parameter properties

Class member cannot have `const` as memeber, Hence it is a typescript type mentioned `readonly`

```ts
class Octopus {
    readonly numberOfLegs: number = 8;
    constructor(readonly name: string) { //readonly is used here
    }
}
```

also `public`, `private` and `prtected` can be used for parameter properties

## Abstract class and methods

Abstract classes are base classes from which other classes may be derived. They may not be instantiated directly.

```ts
abstract class Animal {
    abstract makeSound(): void;
    move(): void {
        console.log("roaming the earth...");
    }
}
```

`abstract method` with in `abstract classes` should not contain the implementation logic

### Difference between abstract methods and interface methods

- Abstract methods share a similar syntax to interface methods. Both define the signature of a method without including a method body.

- However, abstract methods must include the abstract keyword and `may optionally include access modifiers`.

### Example

```ts
abstract class Department {

    constructor(public name: string) {
    }

    printName(): void {
        console.log("Department name: " + this.name);
    }

    abstract printMeeting(): void; // must be implemented in derived classes
}

class AccountingDepartment extends Department {

    constructor() {
        super("Accounting and Auditing"); // constructors in derived classes must call super()
    }

    printMeeting(): void {
        console.log("The Accounting Department meets each Monday at 10am.");
    }

    generateReports(): void {
        console.log("Generating accounting reports...");
    }
}

let department: Department; // ok to create a reference to an abstract type
department = new Department(); // error: cannot create an instance of an abstract class
department = new AccountingDepartment(); // ok to create and assign a non-abstract subclass
department.printName();
department.printMeeting();
department.generateReports(); // error: method doesn't exist on declared abstract type
```
