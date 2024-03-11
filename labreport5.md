# CSE 15L Lab Report 5:
## Hugh Trevor Redford
## A17067426

## Part 1: Debugging Scenario

**Scenario Instructions**

The task for the student is to complete a brief in-class exercise wherein they implement a Selection Sort algorithm for an integer list. Additionally, they need to create a simple test to demonstrate the algorithm's functionality using basic cases.

Furthermore, the student is expected to create a Bash script responsible for compiling and executing the program.

**Student Post/Question**

Hello, I'm currently working on implementing a sorting algorithm, but I'm encountering an unusual issue with my output. The sorted array appears to have identical values, and I suspect the problem might be related to the swapping section of my code. Notably, the first value is 1, which aligns with the expected sorted array at index 0. Below, you'll find my code in a file named Sort.java, along with a Bash script named test.sh that I've created to run it. Any insights would be appreciated.

```
import java.util.ArrayList;

public class Sort{
	
	public static int[] selection(int[] lst) {
		for ( int i = 0; i < lst.length - 1; i++) {
			int min = i; 
			for ( int j = i; j < lst.length; j++ ) {
				if ( lst[min] >=  lst[j] ) {
					min = j;
				}
			}
			lst[i] = lst[min];
		}		
		return lst;
	}
	
	public static void main(String[] args) {
		
		int[] testArr = {9,8,7,6,5,4};
		int[] expectedArr = {1,2,3,4,5,6};
		System.out.println("Test Array:");
		System.out.print("[ ");
		for (int j = 0; j < testArr.length; j++) {
			System.out.print(testArr[j]);
			System.out.print(" ");

		}
		System.out.println("]");
		int[] newArr = selection(testArr);
		for ( int i = 0; i < newArr.length; i ++ ) {
			if ( newArr[i] != expectedArr[i] ) {
				System.out.println("Error! Did not match expected array! ");
				break;
			} 
		}
		System.out.println("Sorted Array:");
		System.out.print("[ ");
		for (int i = 0; i < newArr.length; i++ ) {
			System.out.print(newArr[i]);
			System.out.print(" ");

		}
		System.out.println("]");

	}
}

```
```
javac Sort.java 
java Sort 
```
"I executed the test using the command `bash test.sh`, and the output is as follows:"
```
Test Array:
[ 9 8 7 6 5 4 ]
Error! Did not match expected array! 
Sorted Array:
[ 1 1 1 1 1 1 ]
```

