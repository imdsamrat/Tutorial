# Issues with old Date and Calendar classes

- Mutable
- Confusing
- Limitation (not good at Zone level and time diff)

# New Date and Time classes

- LocalDate
- LocalTime
- LocalDateTime
- ZonedDateTime
- Instant
- Period
- Duration
- DateTimeFormatter

# LocalDate

```java
public class Test {
  public static void main(String[] args) {
    LocalDate today = LocalDate.now();
    System.out.println(now);
    LocaDate customDate = LocalDate.of(1990, 2, 24);

    int dayOfMonth = today.getDayOfMonth();
    String month = today.getMonth();
    int year = today.getYear();
    System.out.println(dayOfMonth);
    System.out.println(month);
    System.out.println(year);

    LocalDate yesterday = today.minusDays(1);
    LocalDate pastMonthDate = today.minusMonths(100);
    LocalDate prevWeekDate = today.minusWeeks(1);
    LocalDate prevYearDate  = today.minusYears(1);

    if(today.isAfter(yesterday)) {
      System.out.println(true)
    }
  }
}
```

> 2023

> JUNE

> 27

> true

# LocalTime

```java
public class Test {
  public static void main(String[] args) {
    LocalTime now = LocalTime.now();
    System.out.println(now);

    LocaTime customTime = LocaTime.of(14, 30, 30);
    System.out.println(customTime);

    String timeInString = "15:30:30";
    LocalTime parsedTime = LocalTime.parse(timeInString);
    System.out.println(parsedTime);

    LocalTime beforeOneHour = now.minusHours(1)
    System.out.println(beforeOneHour);

    if(now.isAfter(beforeOneHour)) {
      System.out.println(true)
    }
  }
}
```

> 15:37:33.613

> 14:30:30

> 13:30:30

> 14 :37:33.613

> true

# LocalDateTime

```java
public class Test {
  public static void main(String[] args) {
    LocalDateTime now = LocalDateTime.now();
    System.out.println(now);

    LocalTime parsedTime = LocalTime.parse("2023-01-11T15:30");
    System.out.println(parsedTime);
  }
}
```

> 2023-06-27T15:37:33.613

> 2023-01-11T15:30

# ZonedDateTime

```java
public class Test {
  public static void main(String[] args) {
    ZonedDateTime now = ZonedDateTime.now();
    ZonedDateTime customZonedDateTime = ZonedDateTime.of(2000, 12, 1, 14, 30, 45, 30, ZoneId.of("America/New_York"));

    ZonedDateTime indiaTime = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));
    ZonedDateTime newYorkTime = ZonedDateTime.now(ZoneId.of("America/New_York"));


  }
}
```

> 2023-06-27T15:37:33.613+05:30[Asia/Kolkata]

> 2000-12-01T14:30:45.030-04:00[America/New_York]

> 2023-06-27T15:37:33.613+05:30[Asia/Kolkata]

> 2023-06-27T06 :07:33.613-04:00[America/New_York]
