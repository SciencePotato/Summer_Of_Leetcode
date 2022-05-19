## [Sqrt(X)](https://leetcode.com/problems/sqrtx/)
The normal solution for any sane human being.
```java
class Solution {
    public int mySqrt(int x) {
        long r = x;
        while (r*r > x)
            r = (r + x/r) / 2;
        return (int) r;
    }
}
```
The binary search method would be.
```java
  public int mySqrt(int x) {
      if (x == 0) return 0;
      int left = 1;
      int right = x;
      int bound = -1;
      while (left <= right) {
          int mid = left + (right - left) / 2;
          if (mid <= x / mid) {
              bound = mid;
              left = mid + 1;
          } else {
              right = mid - 1;
          }
      }
      return bound;
  }
```

## [Subarray Less than K](https://leetcode.com/problems/subarray-product-less-than-k/)
```java
public int numSubarrayProductLessThanK(int[] nums, int k) {
    if(k <= 1) return 0;


    int prod = 1, res = 0, left = 0;


    for(int right = 0; right < nums.length; right++) {

        prod *= nums[right];

        while(prod >= k) {
            prod /= nums[left];
            left++;
        }

        // This is like Combinatorics (Inclusive-Exclusive principles)
        res += right - left + 1;
    }
    return res;
}
```
Everything about this is a standard sliding window problem. The challenges comes in the last part, since we want to increment the combinations by _X_ amount, but there also exists overlaps within the the _X_, so we want to use the inclusive exclusive principles basically.
