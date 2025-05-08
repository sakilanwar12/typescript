

### Blog One ### 

# What are some differences between interfaces and types in TypeScript?

type and interfaces mostly similiar but has a lot of differences,

### The Key Differences (From My Experience)

## 1. Extending Types

```bash
// interface
interface Person {
  name: string;
}
interface Employee extends Person {
  role: string;
}
```
```bash
// type
type Person = {
  name: string;
};
type Employee = Person & {
  role: string;
};

```

### 2. Unions, Primitives, and Tuples? Use type

```
type Status = "idle" | "loading" | "error";

type Primitive = string | number | boolean;

type Point = [number, number];
```

### 3. Utility Types and Mapped Types Work Better with type

```
type User = {
  id: number;
  name: string;
};

type PartialUser = Partial<User>;

```

### 4. Working with Classes? I Go with interface
```
interface Animal {
  name: string;
  speak(): void;
}

class Dog implements Animal {
  name = "Dog";
  speak() {
    console.log("Woof!");
  }
}

```

### 5. So, What Do I Actually Use?

These days, I try to stick to this:

I use interface for describing objects, especially models, components, and anything class-like.

I use type when I need flexibility—unions, conditional types, mapped types, or mixing multiple types together.

Of course, both can work in a lot of situations. But I’ve found that being consistent keeps things clean, especially when working on teams or open-source projects.

Thanks for taking the time to read my thoughts — I really appreciate it! 🙌




________________

## Blog 2

The keyof keyword in TypeScript is used to extract the keys of a given type as a union of string literal types. It's especially useful when you're working with generic types and want to restrict access or create mappings based on the keys of an object.

### 1. keyof helps you refer to the property names of a type as values.
Example:

```
type User = {
  id: number;
  name: string;
  email: string;
};

type UserKeys = keyof User;
// Equivalent to: "id" | "name" | "email"

```

### 2. Practical Example: Accessing Object Properties Safely

```
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const user = {
  id: 1,
  name: "Sakil",
  email: "sakil@example.com",
};

const userName = getProperty(user, "name"); // ✅ "Sakil"
// const invalid = getProperty(user, "age"); ❌ Error: Argument of type '"age"' is not assignable

```

### Why It’s Useful 
- Prevents typos in property names
- Ensures type safety when accessing dynamic keys
- Enables advanced patterns like form validation, dynamic table generation, etc.

