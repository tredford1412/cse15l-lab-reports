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

public class Sort {

    public static int[] selection(int[] lst) {
        for (int i = 0; i < lst.length - 1; i++) {
            int min = i;
            for (int j = i; j < lst.length; j++) {
                if (lst[min] >= lst[j]) {
                    min = j;
                }
            }
            lst[i] = lst[min];
        }
        return lst;
    }

    public static void main(String[] args) {
        int[] testArr = {9, 8, 7, 6, 5, 4};
        int[] expectedArr = {1, 2, 3, 4, 5, 6};

        System.out.println("Test Array:");
        System.out.print("[ ");
        for (int j : testArr) {
            System.out.print(j + " ");
        }
        System.out.println("]");

        int[] newArr = selection(testArr);

        for (int i = 0; i < newArr.length; i++) {
            if (newArr[i] != expectedArr[i]) {
                System.out.println("Error! Did not match expected array!");
                break;
            }
        }

        System.out.println("Sorted Array:");
        System.out.print("[ ");
        for (int value : newArr) {
            System.out.print(value + " ");
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

**TA Response**

Hey there! You're on the right track with your algorithm. It effectively identifies the minimum value. However, it seems there might be an issue with the swapping process. Have you double-checked if your swap operation is actually exchanging the values as intended?

**Student Fix/ Explanation of Bug**

Upon inspecting the algorithm, I realized that the swapping mechanism wasn't functioning as intended. Instead of properly swapping the values, it was merely reassigning the current element to the minimum value, resulting in the loss of the current value. Since the minimum value is at the end of the list, this led to all values being reassigned to 1, failing to sort the list.

To fix this, I introduced a temporary variable named temp. This variable temporarily holds the current value, allowing us to swap the values effectively. Here's the updated code snippet of the selection method:

```
public static int[] selection(int[] lst) {
    for (int i = 0; i < lst.length - 1; i++) {
        int min = i;
        for (int j = i + 1; j < lst.length; j++) {
            if (lst[min] > lst[j]) {
                min = j;
            }
        }
        int temp = lst[i];
        lst[i] = lst[min];
        lst[min] = temp;
    }
    return lst;
}
```
After executing bash test.sh, the output now matches the expected result. Here's the updated output:
```
Test Array:
[ 9 8 7 6 5 4 ]
Sorted Array:
[ 1 2 3 4 5 6 ]
```

## Part 2: Reflection
In the latter part of the quarter, I delved into several valuable topics, among which learning Git and GitHub stood out as the most significant. Conversations with our TA, Andrew, underscored the ubiquity of these tools in the industry, highlighting their importance for aspiring developers. Encouraged by this insight, I embarked on creating my own repositories for CSE 12 PAs. This approach streamlined my workflow, enabling seamless editing across different devices, be it my laptop or home desktop.

Moreover, I tackled Vim, a tool renowned for its complexity yet revered for its command-line prowess. While Vim's intricacies initially seemed daunting, I found it exhilarating to navigate and perform tasks entirely from the command line. Although I grasped the fundamentals of Vim, mastering it promises heightened efficiency and proficiency in command-line operations.

In addition to technical skills, learning the commands of pwd, ls, cd, cat, etc were extremely valuable. I will be using these command for the rest of my computer science journey. 

Reflecting on the course, I am immensely gratified by the wealth of knowledge acquired. Each learning experience, from Git, Vim and basic commands has equipped me with essential tools and insights crucial for success in my journey as a developer.

