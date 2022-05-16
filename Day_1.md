## [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
The question asks for an subarray that contains the maximum value there is. Sliding window technique will not work in this case, so here's comes another algorithm called [Kadane's Algorithm](https://medium.com/@rsinghal757/kadanes-algorithm-dynamic-programming-how-and-why-does-it-work-3fd8849ed73d). Essentially, the idea is that, if it's less than the current sum, you can discard it and continue to increases your sum without worrying about anything.

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int global = nums[0];
        int current = nums[0];
        
        for (int i = 1; i < nums.length; i ++) {
            
            if (current < 0) current = nums[i];
            else current += nums[i];
            
            global = Math.max(global, current);
        }
        
        return global;
    }
}
```

## [Sorting Colors](https://leetcode.com/problems/sort-colors/)
This is a sorting problem, there are many ways to solve this. The two way there is to do this, which I figured out the "Brute force" way was a counting sort. You basically count the amount of element and starting to sorted by then. The other way is Quicksort with 3 pivot or something, more information down below.

The first solution, which require 2-passes (Counting Sort):
```java
class Solution {
    public void sortColors(int[] nums) {
        // 2-Pass, counting sort
        int count0 = 0, count1 = 0, count2 = 0;
        for (int i = 0; i < nums.length; i ++) {
            if (nums[i] == 0)
                count0++;
            else if (nums[i] == 1) 
                count1++;
            else 
                count2++;
        }
        
        for (int i = 0; i < nums.length; i ++) {
            if (count0 != 0) {
                nums[i] = 0; 
                count0 --;
            } else if (count1 != 0) {
                nums[i] = 1;
                count1 --;
            } else {
                nums[i] = 2;
                count2 --;
            }
        }
    }
}

```

3-way Quick partition in quicksort implement in this problem;
```java
class Solution {
    public void sortColors(int[] nums) {
        int p1 = 0, p2 = nums.length - 1, index = 0;
        
        while (index <= p2) {
            
            if (nums[index] == 0) {
                nums[index] = nums[p1];
                nums[p1] = 0;
                p1 ++;
            } else if (nums[index] == 2) {
                nums[index] = nums[p2];
                nums[p2] = 2;
                p2 --;
                index --;
            }
            
            index ++;
        }
        
    }
}
```

## [3-Way QuickSort (Dutch National Flag)](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)
Instead of using a singular number as our pivot point, the 3-way quicksort implements this algorithm with 2 pivot points, so you'll have a range of array such as the following:

a) arr[l..i] elements less than pivot.  
b) arr[i+1..j-1] elements equal to pivot.  
c) arr[j..r] elements greater than pivot.  

More information can be found on links above.


## [Remove Duplicates II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)
This is a two pointer question, meannig, you have to use a left and a right pointer. In this cases, the question can be simplified into, if there isn't duplication, we increase the count (Nondupe) in this case. If then, there's an item (i) that is larger than our current duplication, we can just replace them, otherwise, we will just keep incrementing. 

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int nonDupe = 0;
        for (int i: nums) {
            if (nonDupe < 2 || i > nums[nonDupe - 2])
                nums[nonDupe++] = i;
        }
        return nonDupe;
    }
}
```

## Resources
- [CS Dojo](https://www.youtube.com/watch?v=86CQq3pKSUw)
- [Wikipedia](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
- [Beginner List](https://leetcode.com/discuss/career/448024/Topic-wise-problems-for-Beginners)
- [3-Way QuickSort (Dutch National Flag)](https://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/)
