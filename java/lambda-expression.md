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
