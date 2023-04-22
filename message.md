##Lab Report 2!
---
#Creating a String Server












#Debugging
Let's take a look at some code that has a bug. 

![Code w/ some Bugs](code-with-bug.png)

This code is supposed to change the input array to be in reversed order.
At first glance the code may not look wrong, but lets write a test to see if it works the way that is intended. 
```
@Test 
public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
 ```

When this code is run the result is as expected
> {3}
This is because this array contains only one element so the original order and reveresed order are the same.
Now for another test:
```
@Test
  public void testReversed2(){
    int[] input2 = {43, 91, 0};
    ArrayExamples.reversed(input2);
    assertArrayEquals(new int[]{0, 91, 43}, ArrayExamples.reversed(input2));
  }
```

**Uh Oh!** This test does not give us the expected output
>`Expected output:`
>	{0, 91, 43}
>`Actual output:`
>	{0, 0, 0}	

*Why did it do this?*
Well if we look back to the code we can analyze line by line...
```
 static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
Hmmm... wait! I see multiple issues here; 
- Since the for loop runs through all the elements of the array after the halfway point the new array's values start to go back
- *So we need to fix the max value of i to half the length*
- BUT, if we change that then half of the array is untouched
- *To fix this we can create a new temp variable to hold the value that get changes, then have it moved*
This should look like:
```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length/2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length-i-1] = temp;
    }
  }
```
Now the code runs in a way that swaps the values with the one at the opposite end.
The first and last value get swapped, the second and second to last get swapped and so on till it reaches the middle, where all the values should have been moved.
