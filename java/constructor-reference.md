# Constructor Reference

```java

public class Student {
  private String name;

  public Student(String name) {
    this.name = name;
  }

  public int getName() {
    return this.name;
  }

  public void setName(String name) {
    this.name = name;
  }

}
```

```java
public class Test {
  public static void main(String[] args) {
    List<String> student = Arrays.asList("Ram", "Raj", "Sam");
    List<Student> students = student.stream().map(x -> new Student(x)).collect(Collectors.toList());
  }
}
```

can be converted to

```java
public class Test {
  public static void main(String[] args) {
    List<String> student = Arrays.asList("Ram", "Raj", "Sam");
    List<Student> students = student.stream().map(Student::new).collect(Collectors.toList());
  }
}
```
