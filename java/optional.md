# Optional

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);

    if(name.isPresent()) {
      System.out.println(name.get)
    }

    name.ifPresent(System.out::println);
  }

  public static Optional<String> getName(int id) {
    String name = "Ram";
    return Optional.ofNullable(name);
  }
}
```

> Ram

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);

    if(name.isPresent()) {
      System.out.println(name.get)
    }

    name.ifPresent(System.out::println);
  }

  public static Optional<String> getName(int id) {
    String name = null;
    return Optional.ofNullable(name);
  }
}
```

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);

    if(name.isPresent()) {
      System.out.println(name.get)
    }

    name.ifPresent(System.out::println);
  }

  public static Optional<String> getName(int id) {
    return Optional.empty();
  }
}
```

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);
    String nameTobeUsed = name.orElse("NA");
    System.out.println(nameTobeUsed);
  }

  public static Optional<String> getName(int id) {
    return Optional.empty();
  }
}
```

> NA

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);
    String nameTobeUsed = name.orElseGet(() -> "NA");
    System.out.println(nameTobeUsed)
  }

  public static Optional<String> getName(int id) {
    return Optional.empty();
  }
}
```

> NA

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);
    String nameTobeUsed = name.orElseThrow(() -> new NoSuchElementException());
    System.out.println(nameTobeUsed)
  }

  public static Optional<String> getName(int id) {
    return Optional.empty();
  }
}
```

> NoSuchElementException

can use method reference in place of lambda expression

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> name = getName(2);
    String nameTobeUsed = name.orElseThrow(NoSuchElementException::new);
    System.out.println(nameTobeUsed)
  }

  public static Optional<String> getName(int id) {
    return Optional.empty();
  }
}
```

> NoSuchElementException

```java
public class Test {
  public static void main(String[] args) {
    Optional<String> optional = getName(2);
    Optional<String> optional1 = optional.map(x -> x.toUpperCase());

   optional1.ifPresent(System.out::println);
  }

  public static Optional<String> getName(int id) {
    return Optional.of("Ram");
  }
}
```

> NoSuchElementException
