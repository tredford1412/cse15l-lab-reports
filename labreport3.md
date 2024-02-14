# Lab Report 3:
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
