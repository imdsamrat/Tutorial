# List in Java

The `List` interface in Java provides a way to store the ordered collection. It is a `child interface of Collection`. It is an ordered collection of objects in which duplicate values can be stored. Since List preserves the insertion order, it allows positional access and insertion of elements.

The List interface is found in java.util package and inherits the Collection interface. It is a factory of the `ListIterator` interface. Through the `ListIterator`, we can iterate the list in `forward and backward` directions. The implementation classes of the `List` interface are `ArrayList`, `LinkedList`, `Stack`. ArrayList and LinkedList are widely used in Java programming.

```java
// Creating an object of List interface
// implemented by the ArrayList class
List<Integer> l1 = new ArrayList<Integer>();

// Adding elements to object of List interface
// Custom inputs

l1.add(0, 1);
l1.add(1, 2);

// Now creating another object of the List
// interface implemented ArrayList class
// Declaring object of integer type
List<Integer> l2 = new ArrayList<Integer>();

// Again adding elements to object of List interface
// Custom inputs
l2.add(1);
l2.add(2);
l2.add(3);

// Will add list l2 from 1 index
l1.addAll(1, l2);

// Removes element from index 1
l1.remove(1);


// add at index 1
l1.add(1, 43);

// Replace 0th element with 5 in List 1
l1.set(0, 5);
```

- indexOf(element): Returns the index of the first occurrence of the specified element in the list, or -1 if the element is not found
- lastIndexOf(element): Returns the index of the last occurrence of the specified element in the list, or -1 if the element is not found

```java

import java.util.ArrayList;
import java.util.List;

public class ListExample {
    public static void main(String[] args)
    {
        // create a list of integers
        List<Integer> numbers = new ArrayList<>();

        // add some integers to the list
        numbers.add(1);
        numbers.add(2);
        numbers.add(3);
        numbers.add(2);

        // use indexOf() to find the first occurrence of an
        // element in the list
        int index = numbers.indexOf(2);
        System.out.println(
            "The first occurrence of 2 is at index "
            + index);

        // use lastIndexOf() to find the last occurrence of
        // an element in the list
        int lastIndex = numbers.lastIndexOf(2);
        System.out.println(
            "The last occurrence of 2 is at index "
            + lastIndex);
    }
}
```

## Removing Elements

- remove(Object): This method is used to simply remove an object from the List. If there are multiple such objects, then the first occurrence of the object is removed.
- remove(int index): Since a List is indexed, this method takes an integer value which simply removes the element present at that specific index in the List. After removing the element, all the elements are moved to the left to fill the space and the indices of the objects are updated.

```java
// Java Program to Remove Elements from a List

// Importing List and ArrayList classes
// from java.util package
import java.util.ArrayList;
import java.util.List;

// Main class
class GFG {

	// Main driver method
	public static void main(String args[])
	{

		// Creating List class object
		List<String> al = new ArrayList<>();

		// Adding elements to the object
		// Custom inputs
		al.add("Geeks");
		al.add("Geeks");

		// Adding For at 1st indexes
		al.add(1, "For");

		// Print the initialArrayList
		System.out.println("Initial ArrayList " + al);

		// Now remove element from the above list
		// present at 1st index
		al.remove(1);

		// Print the List after removal of element
		System.out.println("After the Index Removal " + al);

		// Now remove the current object from the updated
		// List
		al.remove("Geeks");

		// Finally print the updated List now
		System.out.println("After the Object Removal "
						+ al);
	}
}
```

## Accessing Elements

- get(int index): This method returns the element at the specified index in the list.

```java
// Java Program to Access Elements of a List

// Importing all utility classes
import java.util.*;

// Main class
class GFG {
	// Main driver method
	public static void main(String args[])
	{
		// Creating an object of List interface,
		// implemented by ArrayList class
		List<String> al = new ArrayList<>();

		// Adding elements to object of List interface
		al.add("Geeks");
		al.add("For");
		al.add("Geeks");

		// Accessing elements using get() method
		String first = al.get(0);
		String second = al.get(1);
		String third = al.get(2);

		// Printing all the elements inside the
		// List interface object
		System.out.println(first);
		System.out.println(second);
		System.out.println(third);
		System.out.println(al);
	}
}
```

## Checking if an element is present in the List

- contains(Object): This method takes a single parameter, the object to be checked if it is present in the list.

```java
// Java Program to Check if an Element is Present in a List

// Importing all utility classes
import java.util.*;

// Main class
class GFG {
	// Main driver method
	public static void main(String args[])
	{
		// Creating an object of List interface,
		// implemented by ArrayList class
		List<String> al = new ArrayList<>();

		// Adding elements to object of List interface
		al.add("Geeks");
		al.add("For");
		al.add("Geeks");

		// Checking if element is present using contains()
		// method
		boolean isPresent = al.contains("Geeks");

		// Printing the result
		System.out.println("Is Geeks present in the list? "
						+ isPresent);
	}
}
```

# Iterating over List Interface in Java

There are multiple ways to iterate through the List. The most famous ways are by using the basic `for` loop in combination with a `get()` method to get the element at a specific index and the advanced for a loop.

```java
// Java program to Iterate the Elements
// in an ArrayList

// Importing java utility classes
import java.util.*;

// Main class
public class GFG {

	// main driver method
	public static void main(String args[])
	{
		// Creating an empty Arraylist of string type
		List<String> al = new ArrayList<>();

		// Adding elements to above object of ArrayList
		al.add("Geeks");
		al.add("Geeks");

		// Adding element at specified position
		// inside list object
		al.add(1, "For");

		// Using for loop for iteration
		for (int i = 0; i < al.size(); i++) {

			// Using get() method to
			// access particular element
			System.out.print(al.get(i) + " ");
		}

		// New line for better readability
		System.out.println();

		// Using for-each loop for iteration
		for (String str : al)

			// Printing all the elements
			// which was inside object
			System.out.print(str + " ");
	}
}
```

## Implementations of List Interface

- ArrayList
- LinkedList
- Stack
- Vector

## ArrayList

An ArrayList class which is implemented in the collection framework provides us with dynamic arrays in Java. Though, it may be slower than standard arrays but can be helpful in programs where lots of manipulation in the array is needed. Let’s see how to create a list object using this class.

```java
// Java program to demonstrate the
// creation of list object using the
// ArrayList class

import java.io.*;
import java.util.*;

class GFG {
	public static void main(String[] args)
	{
		// Size of ArrayList
		int n = 5;

		// Declaring the List with initial size n
		List<Integer> arrli = new ArrayList<Integer>(n);

		// Appending the new elements
		// at the end of the list
		for (int i = 1; i <= n; i++)
			arrli.add(i);

		// Printing elements
		System.out.println(arrli);

		// Remove element at index 3
		arrli.remove(3);

		// Displaying the list after deletion
		System.out.println(arrli);

		// Printing elements one by one
		for (int i = 0; i < arrli.size(); i++)
			System.out.print(arrli.get(i) + " ");
	}
}
```

## LinkedList

LinkedList is a class that is implemented in the collection framework which inherently implements the linked list data structure. It is a linear data structure where the elements are not stored in contiguous locations and every element is a separate object with a data part and address part. The elements are linked using pointers and addresses. Each element is known as a node. Due to the dynamicity and ease of insertions and deletions, they are preferred over the arrays.

```java
// Java program to demonstrate the
// creation of list object using the
// LinkedList class

import java.io.*;
import java.util.*;

class GFG {
	public static void main(String[] args)
	{
		// Size of the LinkedList
		int n = 5;

		// Declaring the List with initial size n
		List<Integer> ll = new LinkedList<Integer>();

		// Appending the new elements
		// at the end of the list
		for (int i = 1; i <= n; i++)
			ll.add(i);

		// Printing elements
		System.out.println(ll);

		// Remove element at index 3
		ll.remove(3);

		// Displaying the list after deletion
		System.out.println(ll);

		// Printing elements one by one
		for (int i = 0; i < ll.size(); i++)
			System.out.print(ll.get(i) + " ");
	}
}
```
