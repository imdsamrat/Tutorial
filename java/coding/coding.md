## Copy an array to a new array

```java
// copy an array to new array

public static void arraycopy(Object source_arr, int sourcePos, Object dest_arr, int destPos, int len)
```

## Clone Array

```java
class Solution {
  public void cloneArray(int[] array) {
    int clonedArray[] = array.clone();
  }
}
```

## Sorting a 2D Array according to values in any given column in Java

```java
public static void sortbyColumn(int arr[][], int col) {
    // Using built-in sort function Arrays.sort with lambda expressions

  Arrays.sort(arr, (a, b) -> Integer.compare(a[col],b[col])); // increasing order

}
```

## Store pair of values in an array

If we need to process an array in which we need to retrieve two values at one place and do some processing. Like, given an array an we want the value arr[i] and arr[n-1-i] at the same time, then we can use this idea to store two value at single place and retrieve later. Without having extra space.

```java
// store pair of values in the array
nums[i] = nums[i] * MAX_LEN + nums[n-1-i];

// retrieve the pair
nums[n-1-i] = nums[i] % MAX_LEN;
nums[i] = nums[i] / MAX_LEN;
```

Here we can use bitwise operator as well.

```java
int MAX_LEN; // power of two greater than length of array.
// store pair of values in the array, if array size is 1000 take MAX_LEN = 1024 and hence power = 10.
int power = log(MAX_LEN);
nums[i] = nums[i] << power | nums[n-1-i];

// retrieve the pair
nums[n-1-i] = nums[i] & (MAX_LEN - 1);
nums[i] = nums[i] >>> power;
```
