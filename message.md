##Lab Report 2!
#Creating a String Server












#Debugging
Let's take a look at some code that has a bug. 

![Code w/ a Bug](code-with-bug.png)

At first glance the code may not look wrong, but lets write a test to see if it works the way that is intended. 
```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
 ```
