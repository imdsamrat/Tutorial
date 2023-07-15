# Stream

Any collection can be converted into stream. After converting we can use declarative and functional programming over it like map(), filter(), reduce() etc.

```java
public class Test {
  // imperative approach
  public static void main(String[] args) {
    int[] array = new int[] {1, 2, 3, 4, 5, 6};
    int sum = 0;
    for(int i = 0; i < array.length; i++) {
      if(array[i] % 2 == 0) {
        sum += array[i];
      }
    }
  }
}
```

can be converted into

```java
public class Test {
  // declarative approach
  public static void main(String[] args) {
    int[] array = new int[] {1, 2, 3, 4, 5, 6};
    int sum = Arrays.stream(array).filter(x-> x%2 == 0).sum();
  }
}
```

## Advantages of Java Stream API

- Readability: Streams provide more readable and expressive way to perform operations on collections. The syntax is more concise and easy to understand, making it easier for other developers to read and maintain the code.
- Flexiblility: Streams allows us to perform a variety of operations like map, filter, reduce without writing multiple loops or methods. This can save time and make the code more flexible.
- Parallelism: Streams can be processed in parallel, which can provide significant performance boost with large collections. With for-loop we would have to write our own multithreaded code to achieve parallelism.
- Encapsulation: Streams encourage encapsulation as we can perform series of operations on a collection without modifying the original data. This can prevent bugs and improve code readability.

# How to create streams

```java
public class Test {

  public static void main(String[] args) {

    // create from collections
    List<String> list = Arrays.asList("Apple", "Banana", "Orange");
    Stream<String> myStream = list.stream();

    // create from array
    String[] array = {"Apple", "Banana", "Orange"};
    Stream<String> arrayStream = Arrays.stream(array);

    // directly create stream
    Stream<Integer> intStream = Stream.of(1, 2, 3);

    // stream of integer from 0 to 100 (Range operation) using seed, unary operator and iterate method
    Stream<Integer> unaryStream = Stream.iterate(0, x -> x + 1).limit(101);

    // create from supplier using generate method
    Stream<String> supplierStream = Stream.generate(() -> "Hello"); // infinite loop

     // create from supplier using generate method
    Stream<String> supplierStream = Stream.generate(() -> "Hello").limit(100); // 100 times
  }
}
```

# Filter Operations

Filter accepts predicate as argument

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74);
    List<Integer> filteredList = list.stream().filter(x -> x % 2 == 0).collect(Collectors.toList());
    System.out.println(filteredList);
  }
}
```

> [ 2, 44, 34, 56, 74 ]

# Map Operations

Map accepts function as argument

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream().map(x -> x / 2).collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 0, 1, 22, 11, 22, 17, 28, 37, 0, 1, 22 ]

# Distinct Operations

Distinct operation removes duplicate items from stream.

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream().map(x -> x / 2).distinct().collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 0, 1, 22, 11, 17, 28, 37 ]

# Sorted Operations

Sorted operation provides sorted items.

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream().map(x -> x / 2).distinct().sorted().collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 0, 1, 11, 17, 22, 28, 37 ]

Descending order using comparator

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream()
    .map(x -> x / 2)
    .distinct()
    .sorted((a, b) -> b - a)
    .collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 37, 28, 22, 17, 11, 1, 0 ]

## Limit operations

Need only two elements

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream()
    .map(x -> x / 2)
    .distinct()
    .sorted((a, b) -> b - a)
    .limit(4)
    .collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 37, 28, 22, 17 ]

## Skip operations

Will skip elements from starting

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream()
    .map(x -> x / 2)
    .distinct()
    .sorted((a, b) -> b - a)
    .limit(4)
    .skip(1)
    .collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

> [ 28, 22, 17 ]

## Peek operations

Peek accepts consumer as argument, it can perform desired operation using elements but can change the element as its a consumer.

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.stream()
    .map(x -> x / 2)
    .distinct()
    .sorted((a, b) -> b - a)
    .limit(4)
    .skip(1)
    .peek(x -> System.out.println(x))
    .collect(Collectors.toList());
  }
}
```

> [ 28, 22, 17 ]

## Series of operations on single stream

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Stream.iterate(0, x -> x + 1)
    .limit(101)
    .skip(1)
    .filter(x -> x % 2 == 0)
    .map(x -> x / 10)
    .distinct()
    .sorted()
    .collect(Collectors.toList());
     System.out.println(list);
  }


}
```

> [ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 ]

## Min, Max, Count, Sum, Avg operations on stream

Here min/max operations return Optional so we use get() method to access the element.

```java
public class Test {

  public static void main(String[] args) {

    Integer min = Stream.iterate(0, x -> x + 1)
    .limit(101)
    .skip(1)
    .filter(x -> x % 2 == 0)
    .map(x -> x / 10)
    .distinct()
    .sorted()
    .min().get();

    System.out.println(min);

    Integer max = Stream.iterate(0, x -> x + 1)
    .limit(101)
    .skip(1)
    .filter(x -> x % 2 == 0)
    .map(x -> x / 10)
    .distinct()
    .sorted()
    .max().get();

    System.out.println(max);

    // comparator in argument
    Integer max = Stream.iterate(0, x -> x + 1)
    .limit(101)
    .skip(1)
    .filter(x -> x % 2 == 0)
    .map(x -> x / 10)
    .distinct()
    .sorted()
    .max((a, b) -> b - a).get();

    System.out.println(max);

    // count returns long data type
    Long count = Stream.iterate(0, x -> x + 1)
    .limit(101)
    .skip(1)
    .filter(x -> x % 2 == 0)
    .map(x -> x / 10)
    .distinct()
    .sorted()
    .count()

    System.out.println(count);
  }
}
```

> [ 0 ]

> [ 9 ]

> [ 0 ]

> 10

# Parallel Stream

Parallel stream should only be used in case of very large collections when there is need of multi-threaded processing. It is not for smaller collections, as it comes with overhead of dividing collections into multiple chunks, processing them separately and again combining all chunks into single collection as result.

```java
public class Test {

  public static void main(String[] args) {

    List<Integer> list = Arrays.asList(1, 2, 44, 23, 45 , 34, 56, 74, 1, 2, 44);
    List<Integer> mappedList = list.parallelStream()
    .map(x -> x / 2)
    .distinct()
    .sorted((a, b) -> b - a)
    .limit(4)
    .collect(Collectors.toList());
    System.out.println(mappedList);
  }
}
```

[ 37, 28, 22, 17 ]

# Java Stream difference between map and mapToObj

The primitive and object versions of data types (i.e. `int` and `Integer`, `double` and `Double`, etc.) are not really compatible with each other in Java. They are made compatible through the extra step of `auto-boxing/unboxing`. Thus, if you have a stream of primitive ints and if you try to use the object versions of `Stream` and `Function` (i.e. `Stream<Integer>` and `Function<Integer, Integer>`), you will incur the cost of boxing and unboxing the elements.

To eliminate this problem, the function package contains primitive specialized versions of streams as well as functional interfaces. For example, instead of using `Stream<Integer>`, you should use `IntStream`. You can now process each element of the stream using `IntFunction`. This will avoid auto-boxing/unboxing altogether.

Thus, whenever you want to process streams of primitive elements, you should use the primitive specialized streams (i.e. `IntStream`, `LongStream`, and `DoubleStream`) and primitive specialized functional interfaces (i.e. `IntFunction`, `IntConsumer`, `IntSupplier`, etc.) to achieve better performance.

One more thing to note is that none of the primitive specialized functional interfaces (such as `IntFunction`, `DoubleFunction`, or `IntConsumer`) extend the non-primitive functional interfaces (i.e. `Function`, `Consumer`, and so on).

`java.util.function` package contains `int`, `double`, and `long` (but no `float`) versions of all the functional interfaces. For example, there is an `IntFunction`, a `DoubleFunction`, and a `LongFunction`, which are `int`, `double`, and `long`, versions of Function. These functions are used along with primitive specialized versions of streams such as `IntStream`, `DoubleStream`, and `LongStream`.

Let's take some examples:

```java
Stream<Object> stream1 = Stream.of(1, 2, 3); //Will compile fine
IntStream intStream1 = IntStream.of(4, 5, 6); //Will compile fine

Stream<Object> stream2 = IntStream.of(4, 5, 6); //Does not compile
Stream<Object> stream3 = IntStream.of(4, 5, 6).mapToObj(e -> e); //mapToObj method is needed
IntStream intStream2 = Stream.of(4, 5, 6).mapToInt(e -> e); //mapToInt method is needed
```
