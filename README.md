# Module0Solutions

# Module 0 Practice Problems

## Problem 1 Loops

Create a program that calculates the sum of all numbers up to the input.

```java
import java.util.Scanner;
public class CalculateSum
{

    public static void main(String args[])
    {
        Scanner input = new Scanner(System.in);

        System.out.print("What is your input? ");
        int inp = input.nextInt();
        
        int sum = 0;
        for (int i = 0; i <= inp; i++) 
        {
            sum += i;
        }
        
        System.out.print("Total Value = " + sum);
        input.close();

    }
    
}
```

## Problem 2 Conditional Statements

Generate 5 random numbers between 1 and 100 using either the rand() or randi() functions. 
For each number genereated:
* A) If the value is less than 10 have the script display the number as is.
* B) If the value is greater than 50 have the script display the number plus 100.
* C) If the value meets neither (A) or (B)'s conditions then display the number minus 100.

```java
import java.util.Random;

public class ConitionalIf {
    public static void main(String args[]) {
        Random rand = new Random();
        int newRand = 0;
        for (int i = 0; i < 5; i++) {
            // Generate random integers in range 0 to 100
            newRand = rand.nextInt(100) + 1;
            // If the value of the number is <10
            if (newRand < 10) {
                // Just display it
                System.out.println("Stays the same: " + newRand);

            }
            // If the value of the number is >50
            else if (newRand > 50) {
                // Display it +100
                System.out.println("Plus 100: " + (newRand + 100));
            } else {
                // Display it -100
                System.out.println("Minus 100: " + (newRand - 100));
            }
        }
    }
}
```

## Problem 3 Recursion

Create a program that solves the Tower of Hanoi game, ie, moves all disks fron A to C, one at a time.
![Tower of Hanoi](https://cdn-media-1.freecodecamp.org/images/0*UB4f9VNg1RRs4k93.png)


```java
class TowerOfHanoi 
{
    static void towerOfHanoi(int n, char from_rod,
                             char to_rod, char aux_rod)
    {
    
        if (n == 0) {
            return;
        }
        towerOfHanoi(n - 1, from_rod, aux_rod, to_rod);
        System.out.println("Move disk " + n + " from rod "
                           + from_rod + " to rod "
                           + to_rod);
        towerOfHanoi(n - 1, aux_rod, to_rod, from_rod);
    
    }
 
    // Driver code
    public static void main(String args[])
    {
        int N = 3;
 
        // A, B and C are names of rods
        towerOfHanoi(N, 'A', 'C', 'B');
    }
}
```

## Problem 4 Double Loops

Find a pair with the given sum in an array.

```text
Input:
 
nums = [8, 7, 2, 5, 3, 1]
target = 10
 
Output:
 
Pair found (8, 2)
or
Pair found (7, 3)
 
 
Input:
 
nums = [5, 2, 6, 8, 1, 9]
target = 12
 
Output: Pair not found
```

Solution:
```java
class Main
{
    // Naive method to find a pair in an array with a given sum
    public static void findPair(int[] nums, int target)
    {
        // consider each element except the last
        for (int i = 0; i < nums.length - 1; i++)
        {
            // start from the i'th element until the last element
            for (int j = i + 1; j < nums.length; j++)
            {
                // if the desired sum is found, print it
                if (nums[i] + nums[j] == target)
                {
                    System.out.printf("Pair found (%d, %d)", nums[i], nums[j]);
                    return;
                }
            }
        }
 
        // we reach here if the pair is not found
        System.out.println("Pair not found");
    }
 
    public static void main (String[] args)
    {
        int[] nums = { 8, 7, 2, 5, 3, 1 };
        int target = 10;
 
        findPair(nums, target);
    }
}
```

## Problem 5 Double Loops + Conditional

Given an integer array, find the maximum product of two integers in it.

```text

A ={-10, -2, 5, 6, -2}

```

Solution
```java
class Main
{
    // A naive solution to finding the maximum product of two integers
    // in an array
    public static void findMaximumProduct(int[] A)
    {
        // base case
        if (A.length < 2) {
            return;
        }
 
        int max_product = Integer.MIN_VALUE;
        int max_i = -1, max_j = -1;
 
        // consider every pair of elements
        for (int i = 0; i < A.length - 1; i++)
        {
            for (int j = i + 1; j < A.length; j++)
            {
                // update the maximum product if required
                if (max_product < A[i] * A[j])
                {
                    max_product = A[i] * A[j];
                    max_i = i;
                    max_j = j;
                }
            }
        }
 
        System.out.print("Pair is (" + A[max_i] + ", " + A[max_j] + ")");
    }
 
    public static void main (String[] args)
    {
        int[] A = { -10, -3, 5, 6, -2 };
 
        findMaximumProduct(A);
    }
}
```

## Problem 6 Strings

Given a string, check if it is a rotated palindrome or not.

For example,

CBAABCD is a rotated palindrome as it is a rotation of palindrome ABCDCBA.
BAABCC is a rotated palindrome as it is a rotation of palindrome ABCCBA.

```java
class Main
{
    // Recursive function to check if `str[low…high]` is a palindrome or not
    public static boolean isPalindrome(String str, int low, int high)
    {
        return (low >= high) || (str.charAt(low) == str.charAt(high) &&
                                isPalindrome(str, low + 1, high - 1));
    }
 
    // Function to check if a given string is a rotated palindrome or not
    public static boolean isRotatedPalindrome(String str)
    {
        // base case
        if (str == null) {
            return false;
        }
 
        // length of the given string
        int n = str.length();
 
        // check for all rotations of the given string if it
        // is palindrome or not
        for (int i = 0; i < n; i++)
        {
            // in-place rotate the string by 1 unit
            str = str.substring(1) + str.charAt(0);
 
            // return true if the rotation is a palindrome
            if (isPalindrome(str, 0, n - 1)) {
                return true;
            }
        }
 
        // return false if no rotation is a palindrome
        return false;
    }
 
    public static void main(String[] args)
    {
        // palindromic string
        String str = "ABCDCBA";
 
        // rotate it by 2 units
        str = str.substring(2) + str.substring(0, 2);
 
        if (isRotatedPalindrome(str)) {
            System.out.println("The string is a rotated palindrome");
        }
        else {
            System.out.println("The string is not a rotated palindrome");
        }
    }
}
```
