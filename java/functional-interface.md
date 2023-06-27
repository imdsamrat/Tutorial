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

# Some Important Types of Functional Interface

- Predicate
- Function
- Consumer
- Supplier
- BiPredicate
- BiFunction
- BiConsumer
- UnaryOperator
- BinaryOperator

# Predicate

Predicate is a functional interface, which represents boolean valued function.

```java
class Main {
  public static void main(String[] args) {
    Predicate<Integer> salaryGreaterThanOneLac = x -> x > 100000;
    System.out.println(salaryGreaterThanOneLac.test(1000000));
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Predicate<Integer> predicate = x -> x > 100000;
    System.out.println(predicate.test(1000000));
    int salary = 100;
    if(predicate.test(salary)) {
      // ...
    }
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
    int sum = numbers.stream().filter(x -> x%2 == 0).mapToInt(n -> n).sum();
  }
}
```

```java
class Main {
  public static void main(String[] args) {
    Predicate<Integer> isEven = x -> x %2 == 0;
    Predicate<String> startsWithLetterV = x -> x.toLowerCase().charAt(0) == 'v';
    Predicate<String> endsWithLetterL = x -> x.toLowerCase().charAt(x.length() - 1) == 'l';
    Predicate<String> and = startsWithLetterV.and(endsWithLetterL);
    System.out.println(and.test('vipul'));
    Predicate<String> or = startsWithLetterV.or(endsWithLetterL);
    System.out.println(or.test('vipuk'));
    System.out.println(startsWithLetterV.negate().test('vipul'));
    // isEqual() is static method in predicate functional interface
    Predicate<Object> equal = Predicate.isEqual("Vipul");
    System.out.println(equal.test('Vipul'));
  }
}
```

> true

> true

> false

> true

# Function

Function is a functional interface, which has single abstract method named `apply()`. Which can do operations.

```java
public class Main {
  public static void main(String[] args) {
    Function<String, Integer> function = x -> x.length();
    System.out.println(function.apply());
  }
}
```

> 5

```java
public class Main {
  public static void main(String[] args) {
    Function<String, String> function2 = x -> x.substring(0, 3);
    System.out.println(function.apply("Vipul"));
  }
}
```

> Vip

```java
public class Main {
  public static void main(String[] args) {
    Function<List<Student>, List<Student>> studentsWithVipAsPrefix = list -> {
      List<Student> result = new ArrayList<>();
      for(Student student : list) {
        if(function2.apply(student.getName()).equalsIgnoreCase("vip")) {
          result.add(student);
        }
      }
      return result;
    }

    Student s1 = new Student(2, "Vipul");
    Student s2 = new Student(3, "Vipulav");
    Student s3 = new Student(1, "Arav");

    List<Student> students = Arrays.asList(s1, s2, s3);
    List<Student> filteredStudents = studentsWithVipAsPrefix.apply(students);

    System.out.println(filteredStudents);
  }
}
```

> [ Vipul, Vipulav ]

## andThen() default method

```java
public class Main {
  public static void main(String[] args) {
    Function<Integer, Integer> function1 = x -> 2 * x;
    Function<Integer, Integer> function2 = x -> x * x * x;
    System.out.println(function1.andThen(function2).apply(3));
    System.out.println(function2.andThen(function1).apply(3));
  }
}
```

> 216

> 54

## compose() default method

```java
public class Main {
  public static void main(String[] args) {
    Function<Integer, Integer> function1 = x -> 2 * x;
    Function<Integer, Integer> function2 = x -> x * x * x;
    System.out.println(function1.andThen(function2).apply(3));
    System.out.println(function2.andThen(function1).apply(3));
    System.out.println(function1.compose(function2).apply(3));

  }
}
```

> 216

> 54

> 54

Note: compose is reverse of andThen()

## identity() static method

```java
public class Main {
  public static void main(String[] args) {
    Function<String, String> identityFunction = Function.identity();

    System.out.println(identityFunction.apply("Vipul"));

  }
}
```

> Vipul

# Consumer

Consumer is a functional interface, which consumes but does not return anything.

```java
public class Main {
  public static void main(String[] args) {
    Consumer<String> consumer = s -> System.out.println(s);
    consumer.accept("Vipul");
  }
}
```

> Vipul

## andThen() method

```java
public class Main {
  public static void main(String[] args) {
    Consumer<List<Integer>> listConsumer1 = list -> {
      for(Integer a : list) {
        System.out.println(a + 100);
      }
    };
    Consumer<List<Integer>> listConsumer2 = list -> {
      for(Integer a : list) {
        System.out.println(a);
      }
    };
    listConsumer1.andThen(listConsumer2).apply(Arrays.asList(1, 2, 3, 4));
  }
}
```

# Supplier

Supplier is a functional interface, which supplies but does not take/accept anything.

```java
public class Main {
  public static void main(String[] args) {
    Supplier<String> supplier = () -> "Vipul";
    System.out.println(supplier.get());
  }
}
```

> Vipul

Note: `BiPredicate`, `BiFunction` and `BiConsumer` just takes two arguments instead of one and performs similar operations.

# UnaryOperator

```java
public class Main {
  public static void main(String[] args) {
    Function<Integer, Integer> function1 = x -> 2 * x;
    Function<String, String> function2 = str -> str.toLowerCase();


    UnaryOperator<Integer> unaryOperator1 = x -> 2 * x;
    UnaryOperator<String> unaryOperator2 = str -> str.toLowerCase();

    System.out.println(unaryOperator1.apply(2));
  }
}
```

> 4

Note: `BinaryOperator` extends `BiFunction`
