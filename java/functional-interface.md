# Functional Interface

Interface having **exactly single abstract method** but can have any number of defaults and static methods. We can invoke lambda expression by using functional interface.

Below is an example of functional interface.

```java
public interface MyInterface {
  public void sayHello(); // single abstract method
}
```

## Functional interface annotation

It informs compiler that the annotated interface is functional interface and restrict other developer to add more abstract method, but there is no boundation on default and static methods. So, if people have already used some lambda expression and some new team member adds another abstract method in the interface then all lambda expression will start throwing error.

```java
@FunctionalInterface
public interface MyInterface {

  // single abstract method
  public void sayHello();

  // default method
  default void sayBye() {
    System.out.println("Bye");
  }

  // static method
  public static void sayOk() {
    System.out.println("Ok");
  }
}
```

## Inheritance in Functional Interface

if **Parent** is functional interface and there is no other abstract method added in **Child** then, **Child** is also a functional interface.

```java
public interface Child extends Parent {

}
```

## Default methods inside interface

Since java 8, we can have concrete method as well inside interface.

```java
interface Parent {
  default void sayHello() {
    System.out.println("Hello");
  }
}

class Child implements Parent {

}

class MyClass {
  public static void main(String[] args) {
    Child c = new Child();
    c.sayHello();
  }
}
```

> Hello

Override default method

```java
interface Parent {
  default void sayHello() {
    System.out.println("Hello");
  }
}

class Child implements Parent {
  @Override
  public void sayHello() {
    System.out.println("Child says hello");
  }
}

class MyClass {
  public static void main(String[] args) {
    Child c = new Child();
    c.sayHello();
  }
}
```

> Child says hello

```java
interface Parent {
  default void sayHello() {
    System.out.println("Hello");
  }
}

class Child implements Parent {
  @Override
  public void sayHello() {
    System.out.println("Child says hello");
  }
}

class MyClass {
  public static void main(String[] args) {
    Parent c = new Child();
    c.sayHello();
  }
}
```

> Child says hello

```java
interface Parent {
  default void sayHello() {
    System.out.println("Hello");
  }
}

class Child implements Parent {
  @Override
  public void sayHello() {
    System.out.println("Child says hello");
  }
}

class MyClass {
  public static void main(String[] args) {
    Parent c = new Parent();
    c.sayHello();
  }
}
```

> Error => Here, Parent is an interface so instance creation is not possible.

## Famous Interview question

```java
interface A {
  default void sayHello() {
    System.out.println("A says hello");
  }
}

interface B {
  default void sayHello() {
    System.out.println("B says hello");
  }
}


class MyClass implements A, B {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.sayHello();
  }
}
```

> Will throw an error, Duplicate default methods named **sayHello** with parameters () and () are inherited from the types A and B

Solution: Override the method inside implementation class using the super reference. Also if there is difference in signature then there won't be any error.

```java
interface A {
  default void sayHello() {
    System.out.println("A says hello");
  }
}

interface B {
  default void sayHello() {
    System.out.println("B says hello");
  }
}


class MyClass implements A, B {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.sayHello();
  }

  @Override
  public void sayHello() {
    A.super.sayHello();
  }
  // or we can provide out own implementation as well
}
```

## Static method inside interface

- Method defined using **static** keyword.
- Static method contains the complete definition of the method.
- Can't be overriden or changed in implementation class.

```java
interface A {
  static void sayHello() {
    System.out.println("A says hello");
  }
}

class MyClass implements A {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.sayHello(); // can't access static member, will give an error
    MyClass.sayHello(); // again can't access static member, will give an error
    A.sayHello(); // success
  }
}
```

Class object can't access static member of interface. Implementation class reference can't access as well. Only way to access is through interface name itself. But a class object can access the default method of interface class.

```java
interface A {
  static void sayHello() {
    System.out.println("A says hello");
  }

  default void sayBye() {
    System.out.println("A says bye");
  }
}

class MyClass implements A {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.sayHello(); // can't access static member, will give an error
    MyClass.sayHello(); // again can't access static member, will give an error
    myClass.sayBye(); // success
    A.sayHello(); // success
  }
}
```

### Overriding static method in implementation class

```java
interface A {
  static void sayHello() {
    System.out.println("A says hello");
  }
}

class MyClass implements A {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    myClass.sayHello(); // can't access static member, will give an error
    MyClass.sayHello(); // again can't access static member, will give an error
    myClass.sayBye(); // success
    A.sayHello(); // success
  }

  static void sayHello() {
    System.out.println("MyClass says hello");
  }
}
```

> MyClass says hello

Note: Implementation class can't see/access static method of the interface. Here it looks like the implementation class has overridden the static method but not in reality. So basically it is like writing a new method. We can do anything with it like remove static keyword, making it private or anything there won't be any error as these two are totally different methods.

### Can an Interface have static main method like in class?

```java


interface MyClass {
  public static void main(String[] args) {
    System.out.println("Hello world!");
  }
}
```

> Hello world!

Yes we can write from Java 8, as it supports static method inside interface.
