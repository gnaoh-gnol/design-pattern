# Factory Method Pattern
Factory Method is a creational design pattern that provides an interface for creating objects in a superclass,
but allow subclasses to alter the type of objects that will be created.
Factory Pattern is used when we have a super class with multiple subclasses and based on input, we need to return 
one of the subclass.
### Applicability
- Use the Factory Method when you don't know beforehand the exact types and dependencies of the objects your code should 
work with.
- Use the Factory Method when you want to provide users of your library of framework 
with a way to extend its internal component.
- Use Factory Method when you want to save system resources by reusing existing objects 
instead of rebuilding them each time.
### Pros and Cons
| Pros                                                                                                                                      | Cons                                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| You avoid tight coupling between the creator and the concrete products.                                                                   | The code may become more complicated since you need to introduce<br/> a lot of new subclasses to implement the pattern. The best case scenario is when you're introducing the pattern into an existing hierarchy of creator classes. | 
| Single Responsibility Principle. You can move the product creation code in to one place in the program, making the code easier to support |                                                                                                                                                                                                                                      |   
| Open/Closed Principle. You can introduce new types of products into the program without breaking existing client code.                    |                                                                                                                                                                                                                                      | 

#### Super class
Super class in factory design pattern can be an interface, abstract class or a normal java class.
```java
public interface Bank {
    String getBankName();
}
```
#### Subclasses
```java
public class TPBank implements Bank {
    @Override
    public String getBankName() {
        System.out.println("Ngân hàng Thương mại Cổ phần Tiên Phong");
    }
}
```
```java
public class VietcomBank implements Bank {
    @Override
    public String getBankName() {
        System.out.println("Ngân hàng thương mại cổ phần Ngoại thương Việt Nam");
    }
}
```
```java
public class Acb implements Bank {
    @Override
    public String getBankName() {
        System.out.println("Ngân hàng thương mại cổ phần Á Châu");
    }
}
```
#### Factory class

```java
public enum BankType {
    VIETCOMBANK, TPBANK, ACB
}
public class BankFactory {
    public static Bank getBank(BankType bankType) {
        switch (bankType) {
            case ACB -> {
                return new Acb();
            }
            case TPBANK -> {
                return new TPBank();
            }
            case VIETCOMBANK -> {
                return new VietcomBank();
            }
            default -> throw new IllegalStateException("This bank type unsupported.");
        }
    }
}
```
#### Client:
```java
public class Client {
    public static void main(String[] args) {
        Bank bank = BankFactory.getBank(BankType.TPBANK);
        System.out.println(bank.getBankName());
    }
}
```