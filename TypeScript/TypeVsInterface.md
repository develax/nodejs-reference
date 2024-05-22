# `type` and `interface`

### Differences and Use Cases

1. **Declaration Merging:**
   - **Interface:** Supports declaration merging, meaning you can define an interface in multiple places, and TypeScript will merge them into a single definition.
     ```tsx
     interface User {
       name: string;
     }

     interface User {
       age: number;
     }

     // This results in a single User interface with both name and age
     const user: User = { name: "John", age: 30 };
     ```
   - **Type:** Does not support declaration merging.
     ```tsx
     type User = {
       name: string;
     };

     type User = {
       age: number;
     }; // Error: Duplicate identifier 'User'.
     ```

2. **Extending and Intersection:**
   - **Interface:** Uses `extends` to create new interfaces based on existing ones.
     ```tsx
     interface User {
       name: string;
     }

     interface Admin extends User {
       role: string;
     }

     const admin: Admin = { name: "John", role: "Admin" };
     ```
   - **Type:** Uses intersections (`&`) to combine multiple types into one.
     ```tsx
     type User = {
       name: string;
     };

     type Admin = User & {
       role: string;
     };

     const admin: Admin = { name: "John", role: "Admin" };
     ```

3. **Union Types:**
   - **Interface:** Cannot create union types.
   - **Type:** Can create union types.
     ```tsx
     type Status = "success" | "error" | "loading";
     ```

4. **Usage Scope:**
   - **Interface:** Mainly used for defining the shape of an object.
     ```tsx
     interface User {
       name: string;
       age: number;
     }
     ```
   - **Type:** Can define object shapes, primitive types, union types, tuples, etc.
     ```tsx
     type User = {
       name: string;
       age: number;
     };

     type ID = string | number;

     type Point = [number, number];
     ```

### Practical Recommendations

- **Use `interface` when:**
  - You expect to use declaration merging.
  - You are defining the shape of objects and need to extend interfaces.

- **Use `type` when:**
  - You need to define union types, tuples, or more complex types.
  - You are defining aliases for primitives, unions, or intersections.
  - You need to use advanced type features like mapped types.

### Example of Combining Both

You can use both `interface` and `type` together to leverage their strengths:

```tsx
interface User {
  name: string;
  age: number;
}

type Role = "admin" | "user";

type UserRole = User & { role: Role };

const userRole: UserRole = {
  name: "Alice",
  age: 25,
  role: "admin",
};
```

### Conclusion

Both `type` and `interface` have their places in TypeScript. Generally, `interface` is preferred for defining object shapes due to its extendability and declaration merging. However, `type` is more versatile for complex types and unions. Choose the one that fits your specific use case best.

### Methods in Interfaces

In TypeScript, both `types` and `interfaces` can define methods, but the way they handle them is slightly different. Here’s a deeper look into how methods are handled in `types` and `interfaces`.

Interfaces can define methods directly within them. Here’s how you can define methods in an interface:

```typescript
interface User {
  name: string;
  age: number;
  greet(): void; // Method declaration
  setAge(age: number): void; // Method declaration with parameters
}

const user: User = {
  name: "Alice",
  age: 25,
  greet() {
    console.log("Hello, my name is " + this.name);
  },
  setAge(age: number) {
    this.age = age;
  },
};
```

### Methods in Types

Types can also define methods, but typically you use object type definitions. Here's how you can do it:

```typescript
type User = {
  name: string;
  age: number;
  greet(): void; // Method declaration
  setAge(age: number): void; // Method declaration with parameters
};

const user: User = {
  name: "Alice",
  age: 25,
  greet() {
    console.log("Hello, my name is " + this.name);
  },
  setAge(age: number) {
    this.age = age;
  },
};
```

### Key Differences

1. **Declaration Merging:**
   - **Interface:** Supports declaration merging, which can be useful if you need to augment an existing interface.
     ```typescript
     interface User {
       name: string;
     }

     interface User {
       greet(): void;
     }

     const user: User = {
       name: "Alice",
       greet() {
         console.log("Hello, my name is " + this.name);
       },
     };
     ```
   - **Type:** Does not support declaration merging.
     ```typescript
     type User = {
       name: string;
     };

     type User = {
       greet(): void;
     }; // Error: Duplicate identifier 'User'.
     ```

2. **Extending/Intersection:**
   - **Interface:** Uses `extends` to create new interfaces from existing ones.
     ```typescript
     interface Person {
       name: string;
     }

     interface User extends Person {
       age: number;
       greet(): void;
     }
     ```
   - **Type:** Uses intersection types to achieve a similar result.
     ```typescript
     type Person = {
       name: string;
     };

     type User = Person & {
       age: number;
       greet(): void;
     };
     ```

### Practical Recommendations

- **Use `interface` when:**
  - You want to take advantage of declaration merging.
  - You are defining the shape of objects that may be extended or implemented by classes.

- **Use `type` when:**
  - You need to define complex types, such as unions or intersections.
  - You are defining aliases for function signatures, unions, or tuples.

### Example Combining Both

You can use interfaces and types together to leverage their respective strengths:

```typescript
interface Person {
  name: string;
  greet(): void;
}

type Age = {
  age: number;
};

type User = Person & Age;

const user: User = {
  name: "Alice",
  age: 25,
  greet() {
    console.log("Hello, my name is " + this.name);
  },
};
```

### Conclusion

Both `interface` and `type` can define methods. Interfaces are often preferred for defining the shape of objects, especially when you want to leverage declaration merging or extend interfaces. Types are more flexible and are often used for complex type definitions involving unions, intersections, or type aliases. Choose based on the specific needs and structure of your code.
