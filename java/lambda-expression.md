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

```java
class Main {
  public static void main(String[] args) {
    List<Integer> list = new ArrayList<>();
    list.add(2);
    list.add(4);
    list.add(77);
    list.add(45);
    list.add(23);
    list.add(298);
    Collections.sort(list)
    System.out.println(list);
  }
}
```

> [ 2, 4, 23, 45, 77, 298 ]

By default it sorts in ascending order.

For descending order or custom sorting, we need to provide another argument `comparator` implementation.

```java
class Main {
  public static void main(String[] args) {
    List<Integer> list = new ArrayList<>();
    list.add(2);
    list.add(4);
    list.add(77);
    list.add(45);
    list.add(23);
    list.add(298);
    Collections.sort(list, (a, b) -> b - a)
    System.out.println(list);
  }
}
```

> [ 298, 77, 45, 23, 4, 2 ]

```java
class Main {
  public static void main(String[] args) {
    Set<Integer> set = new TreeSet<>();
    set.add(22);
    set.add(1);
    set.add(13);
    System.out.println("Before custom sorting: " + set);
    Set<Integer> newSet = new TreeSet<>((a, b) -> b - a);
    newSet.add(22);
    newSet.add(1);
    newSet.add(13);
    System.out.println("After custom sorting: " + newSet);
  }
}
```

> Before custom sorting: [1, 13, 22]

> After custom sorting: [22, 13, 1]

```java
class Main {
  public static void main(String[] args) {
    Map<Integer, String> map = new TreeMap<>();
    map.put(2, "z");
    map.put(3, "f");
    map.put(1, "y");
    System.out.println("Before custom sorting: " + map);
    Map<Integer, String> newMap = new TreeMap<>((a, b) -> b - a);
    newMap.put(2, "z");
    newMap.put(3, "f");
    newMap.put(1, "y");
    System.out.println("Before custom sorting: " + newMap);
  }
}
```

> Before custom sorting: {1=y, 2=z, 3=f}

> After custom sorting: {3=f, 2=z, 1=y}

```java
static class Student {
  public Integer id;
  public String name;

  public Student(Integer id, String name) {
    this.id = id;
    this.name = name;
  }

  public String toString() {
    return this.id + ": " + this.name;
  }
}

class Main {
  public static void main(String[] args) {
    Student s1 = new Student(2, "sam");
    Student s2 = new Student(3, "raj");
    Student s3 = new Student(34, "ram");
    List<Student> list = new ArrayList<Student>();
    list.add(s1);
    list.add(s2);
    list.add(s3);
    Collections.sort(list); // will throw error, need to provide comparator as here is list of Student class objects.
    Collections.sort(list, (a, b) -> b.id - a.id);
    System.out.println(list);
  }
}
```

> [34: ram, 3: raj, 2: sam]

# Anonymous Inner Class similarity with Lambda Expression

```java
interface Employee {
  public String getSalary();
  public String getDesignation();
}

class SoftwareEngineer implements Employee {

  @Override
  public String getSalary() {
    return "10";
  }

  @Override
  public String getDesignation() {
    return "Software Engineer";
  }
}


class Main {
  public static void main(String[] args) {
    Employee employee =  new SoftwareEngineer();
    System.out.println(employee.getSalary());
  }
}
```

> 10

Using anonymous inner class

```java
interface Employee {
  public String getSalary();
  public String getDesignation();
}

class Main {
  public static void main(String[] args) {
    Employee employee =  new Employee() {
      @Override
      public String getSalary() {
        return "10";
      }

      @Override
      public String getDesignation() {
        return "Software Engineer";
      }
    };
    System.out.println(employee.getSalary());
  }
}
```

> 10

Note: Here, we are not instanciating the interface as an interface can't be instanciated. We are creating object using anonymous inner class which contains implementation of the interface.

# Variables in Lambda Expression

```java
interface Employee {
  public String getSalary();
}

class Main {
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {
    int x = 2 // local variable
    Employee employee = () -> {
      x = 3 //  will give an error, variable used in lambda expression should be final or effectively final.
      return "100";
    }
  }
}
```

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2 // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {

    Employee employee = () -> {
      x = 3 //  won't give any error.
      return "100";
    }
  }
}
```

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2 // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {

    Employee employee = () -> {
      int x = 3 //  local variable
      return "100";
    }
  }
}
```

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2 // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {
    int x = 3 //  local variable
    Employee employee = () -> {
      return "100";
    }
  }
}
```

Using anonymous inner class

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2 // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {
    int x = 3; //  local variable to doSomething() method

    Employee employee = () -> {
      int x = 10; // local variable to implementation of getSalary() method
      return "100";
    }

    Employee employee = new Employee() {
      int x = 2; // instance variable of anonymous inner class
      @Override
      public String getSalary() {
        return "100";
      }
    }
  }
}
```

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2; // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {
    int x = 3; //  local variable to doSomething() method

    Employee employee = () -> {
      System.out.println(this.x); // success
      return "100";
    }

    Employee employee = new Employee() {
      int x = 2; // instance variable of anonymous inner class
      @Override
      public String getSalary() {
        System.out.println(this.x); // success
        return "100";
      }
    }
  }
}
```

```java
interface Employee {
  public String getSalary();
}

class Main {
  int x = 2; // instance variable
  public static void main(String[] args) {
    doSomething();
  }

  public void doSomething() {
    int x = 3; //  local variable to doSomething() method

    Employee employee = () -> {
      System.out.println(this.x); // success
      return "100";
    }

    Employee employee = new Employee() {
      @Override
      public String getSalary() {
        System.out.println(this.x); // error there is no instace variable named x in anonymous inner class
        return "100";
      }
    }
  }
}
```
