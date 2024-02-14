# CSE 15L Lab Report 3:
## Hugh Trevor Redford
## A17067426

## Part1
The bug I'm choosing takes in an array, and reverses it, which is from the reverseInPlace method.

```
public void testReverseInPlace() {
  int[] input1 = {1,2,3,4,5};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{5,4,3,2,1}, input1);
}
```
This test is intended to assess the method's functionality with a straightforward input to confirm its basic operation. However, the current outcome indicates a failure, as the observed output is ```{5, 4, 3, 4, 5}```.
```
public void testReverseInPlace() {
  int[] input1 = {1,2,2,1};
  ArrayExamples.reverseInPlace(input1);
  assertArrayEquals(new int[]{1,2,2,1}, input1);
}
```
This test does not result in a failure due to the symmetric nature of the array. When iterating through the second half of the array, if the method unintentionally mirrors the first half, it effectively reproduces the original array.

![image](lr3code.png)
The screenshot illustrates both unsuccessful and successful inputs. The issue is due to the method producing 4 instead of the anticipated 2.

## Code Before
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length; i += 1) {
  arr[i] = arr[arr.length - i - 1];
  }
}
```
## Code After
```
static void reverseInPlace(int[] arr) {
  for(int i = 0; i < arr.length / 2; i += 1) {
    int temp = arr[i];
    arr[i] = arr[arr.length - i - 1];
    arr[arr.length - i - 1] = temp;
  }
}
```
This code begins by initializing a temporary integer using the variable `i` within the loop. It then proceeds to swap the element on the opposite side, followed by swapping the temporary element with its corresponding element. Notably, the iteration covers only half of the list, ensuring that the resulting output doesn't merely resemble a mirrored list.

## Part 2:
## Find Command
The find command is an extremely useful way to find specific files or directories. The ```type``` option enables the identification of items based on their characteristics, such as directories (designated by 'd'), files ('f'), and so on.

Executing the command ```find ./technical -type d``` generates a list of directories within the ```./technical``` directory.
The resulting output is:
```
./technical
./technical/government
./technical/government/About_LSC
./technical/government/Env_Prot_Agen
./technical/government/Alcohol_Problems
./technical/government/Gen_Account_Office
./technical/government/Post_Rate_Comm
./technical/government/Media
./technical/plos
./technical/empty
./technical/biomed
./technical/911report
```
Subsequently, when running the command ```find ./technical -type f```, an extensive output of files located in the ```./technical``` directory is obtained. Here is a brief excerpt.
```
./technical/biomed/1471-2199-2-6.txt
./technical/biomed/bcr567.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/biomed/1471-2121-2-3.txt
./technical/biomed/1471-213X-1-11.txt
./technical/biomed/1472-684X-1-5.txt
./technical/biomed/1476-4598-1-6.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
Utilizing this option proves highly beneficial as it aids in identifying directories within directories containing numerous files.

The ```-size``` option facilitates the discovery of files or directories based on their specified size. In the following example, I am searching for files smaller than 10KB within the ```./technical` directory.```

Executing the command ```% find ./technical/911report -size -10k``` will provide the corresponding output.
```
./technical/911report
./technical/911report/preface.txt
```
In this next example, we are identifying files with a size of less than 1MB. The command ```% find ./technical/911report -size -1M``` is employed for this purpose.
The resulting output:
```
./technical/911report
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
```
Observing the two distinct outputs, it's evident that employing this option enables the identification of substantial files that might be consuming excessive space in a specific drive. This, in turn, empowers users to maintain a more efficient and healthier file system.

The ```-empty``` option provides users with the capability to search for empty files or directories. This functionality proves valuable in file management, allowing the identification and deletion of unused files or directories. The accompanying screenshot below illustrates an example of using this option. I've introduced a directory named ```/empty``` within the ```./technical``` directory, containing an empty file to demonstrate the effectiveness of this command.

Executing the command ```% find ./technical -empty``` produces the respective output.
```
./technical/empty/empty.txt
```
The empty text file I introduced to the created ```/empty``` directory is identified as part of the output.

Subsequently, upon deleting the `empty.txt` file, the command ```% find ./technical -empty``` can be employed again. However, the resulting output would now reflect an empty directory, demonstrating the absence of files within the specified directory.
```
./technical/empty
```
This option proves valuable in identifying and eliminating empty files/directories, especially when dealing with a cluttered file system.

The ```-depth``` option facilitates the retrieval of a sorted list of files displayed in the command line. It locates files at the deepest level first and prints them until reaching the specified parent directory.

For instance, running the command ```% find ./technical -depth``` in the ```./technical``` directory generates an output presenting all files and directories in a sorted manner. A brief snippet of the output is provided below.
```
./technical/biomed/bcr567.txt
./technical/biomed/gb-2002-3-10-research0055.txt
./technical/biomed/1471-2121-2-3.txt
./technical/biomed/1471-213X-1-11.txt
./technical/biomed/1472-684X-1-5.txt
./technical/biomed/1476-4598-1-6.txt
./technical/biomed
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-1.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-9.txt
./technical/911report/chapter-8.txt
./technical/911report/preface.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
./technical/911report
./technical
```
As an additional example, executing the command ```% find ./technical/911reports/chapter*.txt -depth``` will output all files matching the specified pattern in a sorted order, organized based on the directory structure. This approach proves beneficial in locating the latest files within a directory, particularly when the directory contains a substantial number of files.
```
./technical/911report/chapter-1.txt
./technical/911report/chapter-10.txt
./technical/911report/chapter-11.txt
./technical/911report/chapter-12.txt
./technical/911report/chapter-13.1.txt
./technical/911report/chapter-13.2.txt
./technical/911report/chapter-13.3.txt
./technical/911report/chapter-13.4.txt
./technical/911report/chapter-13.5.txt
./technical/911report/chapter-2.txt
./technical/911report/chapter-3.txt
./technical/911report/chapter-5.txt
./technical/911report/chapter-6.txt
./technical/911report/chapter-7.txt
./technical/911report/chapter-8.txt
./technical/911report/chapter-9.txt
```
The source I utilized for this lab report is https://ss64.com/bash/find.html
I found this source on a google search and it was extremely helpful in teaching information about the find function. 
