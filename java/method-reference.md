# Method Reference

```java
public class Test {

  public static void print(String s) {
    System.out.println(s);
  }

  public static void main(String[] args) {
    List<String> student = Arrays.asList("Ram", "Raj", "Sam");
    student.forEach(x -> System.out.println(x));
  }
}
```

can be converted to

```java
public class Test {

  public static void print(String s) {
    System.out.println(s);
  }

  public static void main(String[] args) {
    List<String> student = Arrays.asList("Ram", "Raj", "Sam");
    student.forEach(Test::print);
  }
}
```

if `print()` method is not static

```java
public class Test {

  public void print(String s) {
    System.out.println(s);
  }

  public static void main(String[] args) {
    List<String> student = Arrays.asList("Ram", "Raj", "Sam");
    Test test = new Test();
    student.forEach(test::print);
  }
}
```
