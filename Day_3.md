## Sqrt(X) 
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
