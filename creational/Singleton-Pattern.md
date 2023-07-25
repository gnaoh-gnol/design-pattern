# Singleton Pattern
Singleton Pattern says that just "define a class that has only one instance and provides a global point of access to it".
In other words, a class must ensure that only single instance should be created and single object can be used by all other classes.
Examples of Singleton in general usage: Runtime.getRuntime(), Spring Bean, Logger
### Advantages of Singleton design pattern:
- Saves memory because object is not created at each request. Only single instance is reused again and again.
### Disadvantages of Single design pattern:
Although the Singleton pattern is helpful in many cases where you want to set a limit to the instance creation, offering 
some advantages like lazy initialization, controlled access, ect., there are some disadvantages of this design pattern:
1. The global nature leads to dependency hiding.
The Singleton pattern makes it difficult to identify the Instance in its calling class. As you pass the dependencies 
through constructors, the singleton objects becomes directly accessible without being passed through the constructors.
As the code grows, it becomes difficult to identify how different object are related. This thing can confuse any 
new programmer and create ambiguities.
When creating the object of a Singleton class, you do not know its dependencies as the constructor does not have them.
However, inside, there is a dependency on another object. This way, the Singleton leads to dependency hiding.
    ```java
    public class AnObject {
        private SomeOtherObject someObj = SomeOtherObject.GetInstance();
        public AnObject() {
            // nothing here
        }    
    }
    ```
    Solution: This way, the user of your code can see all the dependencies instantly without watching the source code.
This approach also known as Dependency Injection.
    ```java
    public class AnObject {
        private final SomeOtherObject someObject;
        public AnObject(SomeOtherObject objectFromOutSide) {
            this.someObject = objectFromOutSide;
        }    
    }
    ```
2. It can be difficult to unit test the code:
As the Singleton only allows a single instance creation, it is difficult to unit test the code as it requires creating 
more instance.  
As you might know, Singletons are used a lot of database connections or for writing data to files. So, you would not
want your unit tests to access those. Instead, you will try to mock out the object ti perform operations in the memory 
so that you can verify them without having any side effects. The unit tests are supposed to be self-contained 
and must not have connections to the database or some other files that might cause your tests to fail.

    Solution: Unit testing the Singleton objects can seem difficult, but it's not impossible. There are three amazing
approaches that you can take to make unit testing easier with singletons:
   - Create wrapper class and use dependency injection. See: 
   - Use static func property.
   - Use the Extract and override call.

3. It can lead to tightly coupled code:
A code that uses a Singleton class is difficult to change as it exposes its properties and method through a static 
interface making it tightly coupled to its implementation.
4. If the single Instance of the object becomes corrupted, the entire system is compromised.
The singleton objects are generally used in system-level parts of your code, such as database connections or file handlers.
So, if any of these system-wide blocks becomes corrupted, it will affect the entire code base, making the system compromised.

### Applicability
Use the Singleton pattern when a class in your program should have just a single instance available to all clients;
for example, single database object shared by different parts of the program.
Use the Singleton pattern when you need stricter control over global variables. 

### Singleton Pattern Principles:
- Singleton pattern restricts the instantiation of a class and ensures that only one instance of the class exists
in the Java Virtual Machine.
- The singleton class must provide a global access point to get the instance of the class.
- Singleton pattern is used for logging, drivers object, caching and thread pool.
- Singleton design pattern is also used in other design patterns like Abstract Factory, Builder, Prototype, Facade, ect.
- Singleton design pattern is used fin core Java classes also (for example: java.lang.Runtime, java.awt.Desktop).
### Java Singleton Pattern Implementation: 
To implement a singleton pattern, we have different approaches, but all of them have follow common concept:
- Private constructor to restrict instantiation of the class from other classes.
- Private static variable of the same class that is the only instance of the class.
- Public static method that returns the instance of the class, this is the global access point for the outer world
to get the instance of the singleton class.

1. Eager initialization:
2. Static block initialization:
3. Lazy initialization:
Lazy initialization method to implement the singleton pattern, creates the instance in the global access method.
The preceding implementation works fine in the case of the single-threaded environment, but when it comes to 
multithreaded systems, it can cause issues if multiple threads are inside the if condition at the same time.
```java
public class LazyInitializedSingleton() {
    private static LazyInitializedSingleton instance;
    private LazyInitializedSingleton() {}
    public static LazyInitializedSingleton getInstance() {
        if (instance == null) {
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```
4. Thread Safe Singleton:
5. Bill Pugh Singleton:
6. Using reflection to destroy singleton pattern
7. Enum singleton:
8. Serialization and Singleton: