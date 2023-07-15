## Split a string containing multiple words

# StringTokenizer Class in Java

StringTokenizer class in Java is used to break a string into tokens.

This class is used for parsing data. To use String Tokenizer class we have to specify an input string and a string that contains delimiters. Delimiters are the characters that separate tokens. Each character in the delimiter string is considered a valid delimiter. Default delimiters are whitespaces, new line, space, and tab.

- StringTokenizer(String str): default delimiters like newline, space, tab, carriage return, and form feed.
- StringTokenizer(String str, String delim): delim is a set of delimiters that are used to tokenize the given string.
- StringTokenizer(String str, String delim, boolean flag): The first two parameters have the same meaning wherein The flag serves the following purpose.

```java
// If the flag is false, delimiter characters serve to separate tokens

Input : if string --> "hello geeks" and Delimiter is " ", then
Output:  tokens are "hello" and "geeks".

// If the flag is true, delimiter characters are considered to be tokens
Input : String --> is "hello geeks"and Delimiter is " ", then
Output: Tokens --> "hello", " " and "geeks".

// Multiple delimiters can be chosen for a single string
Syntax:
StringTokenizer st1 = new StringTokenizer( "2+3-1*8/4", "+*-/");
Input : String --> is "2+3-1*8/4" and Delimiters are +,*,-,/
Output: Tokens --> "2","3","1","8","4".
```

```java
// Java Program to Illustrate StringTokenizer Class

// Importing required classes
import java.util.*;

// Main class
public class GFG {

	// Main driver method
	public static void main(String args[])
	{

		// Constructor 1
		System.out.println("Using Constructor 1 - ");

		// Creating object of class inside main() method
		StringTokenizer st1 = new StringTokenizer(
			"Hello Geeks How are you", " ");

		// Condition holds true till there is single token
		// remaining using hasMoreTokens() method
		while (st1.hasMoreTokens())

			// Getting next tokens
			System.out.println(st1.nextToken());

		// Constructor 2
		System.out.println("Using Constructor 2 - ");

		// Again creating object of class inside main()
		// method
		StringTokenizer st2 = new StringTokenizer(
			"JAVA : Code : String", " :");

		// If tokens are present
		while (st2.hasMoreTokens())

			// Print all tokens
			System.out.println(st2.nextToken());

		// Constructor 3
		System.out.println("Using Constructor 3 - ");

		// Again creating object of class inside main()
		// method
		StringTokenizer st3 = new StringTokenizer(
			"JAVA : Code : String", " :", true);

		while (st3.hasMoreTokens())
			System.out.println(st3.nextToken());
	}
}
```

## StringTokenizer methods:

- countTokens(): Returns the total number of tokens present
- hasMoreToken(): Tests if tokens are present for the StringTokenizer’s string
- nextElement(): Returns an Object rather than String
- hasMoreElements(): Returns the same value as hasMoreToken
- nextToken(): Returns the next token from the given StringTokenizer.
