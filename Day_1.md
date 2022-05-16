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

## Resources
- [CS Dojo](https://www.youtube.com/watch?v=86CQq3pKSUw)
- [Wikipedia](https://en.wikipedia.org/wiki/Maximum_subarray_problem)
