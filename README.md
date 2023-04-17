# HeadFirst Java, Chapters 7, 8, 9, & 10

Sebastián Zavala Villagómez

---

## Chapter 7: Inheritance and Polymorphism
### Subclasses
- Subclasses inherit from the *superclass*.
- Subclasses extend the *superclass*.
- Subclasses can add new *methods* and instance variables, as well as override inherited *methods*.
- Subclasses can override inherited *methods*.
- Subclasses do not override instance variables.
- Consider the following concepts when building an *inheritance tree*:
    1. Look for objects that have common attributes and *behaviours*.
    2. Design a class that represents the common state and *behaviour*.
    3. Decide if a *subclass* needs *behaviours* that are specific to that particular *subclass* type.
    4. Look for more opportunities to use abstraction, by finding two or more *subclasses* that might need common *behaviour*.
- The `final` keyword in a class definition restricts it from being extended, by which it is "end of the line".
- The JVM will search from lower tiers to higher tiers in the *inheritance tree* for called *methods*.
### IS-A and HAS-A
- ***IS-A***: When one class inherits from another, which applies anywhere in the *inheritance tree*.
- ***HAS-A***: When two classes have a relationship through references without extending.
### Use vs. Abuse
Consider the following when determining if use of inheritance is being used properly or poorly:
- **Do...**:
    - when one class is a more specific type of a *superclass*.
    - when you have *behaviour* that should be shared among multiple classes of the same general type.
- **Do not...**:
    - just to reuse code from another class when the one of the two above rules are violated.
    - if the *subclass* and *superclass* do not pass the IS-A test.
### Inheritance Benefits
- Avoiding the use of duplicate code.
- A common protocol for a group of *classes* is established.
- Guarantee that all *classes* grouped under a certain supertype have all the *methods* that the supertype has.
### Polymorphism
- When a *supertype* is defined for a group of *classes*, any *subclass* of that *supertype* can be sustituted where the *supertype* is expected. 
- With *polymorphism*, the reference type can be a *superclass* of the actual object type.
- *Polymorphism* allows for polymorphic arguments and return types.
- *Polymorphism* allows for writing code that doesn't need to change when introducing new *subclasses*.
### Overriding
- ***Override***: When a *subclass* redefines one of its inherited *methods* when it needs to change or extend the *behaviour* of that *method*.
- Rules:
    1. Arguments must be the same, and return types must be compatible.
    2. The *method* can't be less accessible.
### Overloading
- ***Overload***: Having two or more *methods* with the same name, but difference argument lists. 
- Rules:
    1. The return types can be different.
    2. You can't change **only** the return type.
    3. The access leves can be varied in any direction.

---

## Chapter 8: Interfaces and Abstract Classes
### Abstraction
#### Classes
- Marking *class* as `abstract` blocks being able to create an instance of the *class* in question, requiring it to be extended.
- *Abstract classes* can still be used as a *reference type*.
- *Concrete classes* are classes that are specific enough to be instantiated.
- *Abstract classes* have virtually no use, no value, nor purpose unless they are extended.
- Actual work is done through instances of *subclasses* of the *abstract class*.
- You cannot make a new instance of an *abstract type*, but you **can** make an array object to **hold** that type.
- *Java* does not support *multiple inheritance* with the goal to prevent a problem known as *The Deadly Diamond of Death*.
#### Methods
- *Abstract methods* must overriden.
- The first *concrete class* in the *inheritance tree* must implement all *abstract methods*.
- *Abstract classes* can have both *abstract* and *concrete* *methods*.
- You can call a *method* on an *object* **only** if the *class* of the *reference variable* has that *method*.
- Versions of *inherited methods* from a *superclass* can be invoked in a *method* meant to override the *inherited method*, such as in a case where you only need to add to the existing *method* instead of replacing it completely. This is done by invoking the *superclass*'s version in the new *method*.
### Objects
- An *object* contains **everything** it inherits from each of its *superclasses*.
- *Objects* can be casted back to their real *type*.
### Object Class
- Every *class* in Java extends class *Object*, being the *superclass* of all *superclasses*.
- Any *class* that doesn't **explicitly** extend another *class*, implicitly extends *Object*.
- *Object* is *non-abstract class* because it's got *method* implementation code that all *classes* can use out-of-the-box, without having to override the *methods*.
- Some *Object* *methods* can be overriden. Others are marked as *final*.
- Objects come out of an `ArrayList<Object>` as generic instances of the *Object class*, as the compiler cannot assume the object that comes out is of any type other than *Object*.
- Every *object*, regardless of actual *class type*, is also an instance of *Object class*, by which you can treat the *object* as either its actual *class type* or an *Object*.
- Using *generic type parameters*, you can specify the type of elements that will be stored in an `ArrayList`, which is done by implicitly casting the type automatically for you, as well as providing a compilation error if there are issues with the type.
### Compiler Considerations
- The compiler decides whether you can call a *method* based on the *reference type* instead of the actual *object type*.
### Interfaces
- ***Interface***: A pure *abstract class* that gives many of the polymorphic benefits of *multiple inheritance* without the issues associated. These contain *abstract methods* that must be overriden by classes that implement the *interface*, therefore allowing for enforced sshared *behaviour*.
- *Classes* can implement multiple *interfaces*. 
- When implementing an *interface* as a *polymorphic type*, the *objects* can be from **anywhere** in the *inheritance tree*. The only requirement is that the *objects* are from a *class* that implements the *interface*.

---

## Chapter 9: Constructors and Garbage Collection
### The Stack and the Heap
- ***The Stack***: Where method invocations and local variables live.
- ***The Heap***: Where **all** *objects* live.
- ***Instance Variables***: *Variables* that are declared inside a *class*, but **not** inside a *method*. These live as long as the *object* does. If the *object* is alive, so are its *instance variables*.
- ***Local Variables***: *Variables*, both *primitive* and *reference*, that are declared inside a *method*, including *method parameters*. These live **only** within the *method* that declared the *variable*.
    - ***Life***: A *local variable* is alive as long as its *Stack frame* is on the *Stack*, being until the *method* completes.
    - ***Scope***: A *local variable* is in *scope* only within the *method* in which the *variable* was declared. When its own *method* calls another, the *variable* is alive, but not in *scope* until its *method* resumes. You can use a *variable* only when it is in *scope*.
- The *method* on the top of the *stack* is **always** the *currently executing method*.
- 3 Steps of *Object* Declaration, Creation, and Assignment:
    1. Declare a *reference variable*.
    2. Create an *object*.
    3. Link the *object* and the *reference*.
### Constructors
- ***Constructor***: Contains the code that runs when you instantiate an *object*, as in whenever `new` is used on a *class type*.
- **Only** if a *constructor* is not defined, a default one with no parameters will be created.
- *Constructors* can be overloaded to allow for different implementations for the same *type*.
- *Constructors* are not *inherited*. All the *constructors* in an *object*'s *inheritance tree* must run when you make a new *object*. The call to `super()` must be the first statement in each *constructor*.
- *Constructors* can be overloaded with `this()`, but it must be the first statement in the new *constructor*.
- Every *constructor* can have a call to `super()` or `this()`, but never both.

---

## Chapter 10: Numbers and Statics
### Math Methods
- *Methods* in the *Math class* don't use any *instance variable values*. Since these are *static*, an *instance* of *Math* is unnecessary. Only the *Math class* itself is needed.
### Regular Methods
***Regular Method***: A *method* that requires an *instance* of the *class* to be utilised on.
### Static Methods
- ***Static Method***: A *method* that can be run without any *instance* of the *class*.
- ***Static Variable***: A shared *variable* whose value is the same for **all** *instances* of the *class*.
- ***Static Initialiser***: A block of code that runs when a *class* is loaded, before any other code can use the *class*.
- *Static methods* can't use *non-static (instance) variables*.
- *Static methods* can't use *non-static methods*.
- All *static variables* are initialised in a *class* before any *object* of the *class* can be created.
- *Static final variables* are *constants*.
### Final Keyword
- *Final variables*' values cannot be changed.
- *Final methods* cannot be overridden.
- *Final classes* cannot be extended.
### Wrapper Classes
- All *primitive types* have *wrapper classes* that allow them to be manipulated as *objects*.
- The *wrapper classes* have useful *static methods* to manipulate the *objects*.
