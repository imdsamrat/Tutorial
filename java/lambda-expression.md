# Lambda expression

An anonymous function with

- no name
- no return type
- no modifier

### Steps to make any fuction a lambda expression

- remove modifier
- remove return type
- remove method name
- place arrow

#### Examples

- ```java
  private void sayHello() {
    System.out.println("Hello World!");
  }
  ```

  can be converted into

  ```java
  () -> {System.out.println("Hello World!");}
  ```

- ```java
  private void add(int a, int b) {
    System.out.println(a + b);
  }
  ```

  can be converted into

  ```java
  (int a, int b) -> {System.out.println(a + b);}
  ```

- ```java
  private int getStringLength(String str) {
    return str.length();
  }
  ```

  can be converted into

  ```java
  (String str) -> {return str.length();}
  ```

  can be converted into

  ```java
  (String str) -> return str.length();
  ```

### Use type inference, compiler guess the situation or context.

- ```java
  private void add(int a, int b) {
    System.out.println(a + b);
  }
  ```

  can be converted into

  ```java
    (int a, int b) -> {System.out.println(a + b);}
  ```

  converted into

  ```java
    (a, b) -> System.out.println(a + b);
  ```

### No return keyword

- ```java
  private int getStringLength(String str) {
    return str.length();
  }
  ```

  can be converted into

  ```java
  (String str) -> {return str.length();}
  ```

  can be converted into

  ```java
  (String str) -> return str.length();
  ```

  can be converted into

  ```java
  (str) -> str.length();
  ```

### If only one param remove small brackets

- ```java
  private int getStringLength(String str) {
    return str.length();
  }
  ```

  can be converted into

  ```java
  (String str) -> {return str.length();}
  ```

  can be converted into

  ```java
  (String str) -> return str.length();
  ```

  can be converted into

  ```java
  (str) -> str.length();
  ```

  can be converted into

  ```java
  str -> str.length();
  ```

## Benefits of Lambda Expression

- To enable functional programming in java
- To make code more readable, maintainable and concise code
- To enable parallel processing
- JAR file size reduction
- Elimination of shadow variables

# Where & How to use Lambda Expression

We use lambda expression in functional interface implementation

```java
// Functional Interface
interface Employee {
  public String getName();
}

class SoftwareEngineer implements Employee {
  @Override
  public String getName() {
    return "Software Engineer";
  }
}

class MyClass implements A {
  public static void main(String[] args) {
    Employee employee = new SoftwareEngineer();
    System.out.println(employee.getName());
  }
}
```

can be converted into

```java
// Functional Interface
interface Employee {
  public String getName();
}

class MyClass implements A {
  public static void main(String[] args) {
    Employee se = () -> "Software Engineer";
    System.out.println(se.getName());
  }
}
```

We don't need to create multiple implementation class for different types of employee in case of `Employee as functional interface`.

```java
// Functional Interface
interface Employee {
  public String getName();
}

class MyClass implements A {
  public static void main(String[] args) {
    Employee se = () -> "Software Engineer";
    System.out.println(se.getName());
    Employee editor = () -> "Editor";
    System.out.println(editor.getName());
    Employee manager = () -> "Manager";
    System.out.println(editor.manager());
  }
}
```

Note:

- Interface reference can be used to hold lambda expression
- Using lambda expression we don't need to use any separate implementation class

# Runnable Functional Interface (Create thread using lambda expression)

```java
// Here Runnable is a functional interface used to create thread

class MyClass implements Runnable {

  @Override
  public void run() {
    for(int i = 0; i <  10; i++) {
      System.out.println("Hello " + i);
    }
  }
}

class Main {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    Thread thread = new Thread(myClass);
    thread.run();
  }
}
```

Runnable interface should be implemented by any class whose instances are intended to be executed by a thread. The class must define a method of no arguments called `run`.

Mutithreaded execution

```java
// Here Runnable is a functional interface used to create thread

class MyClass implements Runnable {

  @Override
  public void run() {
    for(int i = 0; i <  10; i++) {
      System.out.println("Hello " + i);
    }
  }
}

class Main {
  public static void main(String[] args) {
    MyClass myClass = new MyClass();
    Thread childThread = new Thread(myClass);
    childThread.run();
    for(int i = 0; i <  10; i++) {
      System.out.println("Hello " + i);
    }
  }
}
```

Now, we want to use lambda expression i.e. without any implementation class.

```java
class Main {
  public static void main(String[] args) {
    Runnable runnable = () -> {
        for(int i = 0; i <  10; i++) {
        System.out.println("Hello " + i);
      };
    Thread thread = new Thread(runnable);
    thread.run();
  }
}
```

or

```java
class Main {
  public static void main(String[] args) {
    Thread thread = new Thread(() -> {
        for(int i = 0; i <  10; i++) {
        System.out.println("Hello " + i);
      }
    });
    thread.run();
  }
}
```

# Comparator Functional Interface
