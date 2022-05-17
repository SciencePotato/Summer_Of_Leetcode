## [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) 

Solution found on the Discussion posted. Its using two pointer from the end, and decrementally compare to one another and just replace it in place. When everything is done, there might be room left in Tail2, or in Array 2 since Array 1 > Array 2. At that point, you just have to add it to your array and everything would be done.
```java
// Two Pointer
int tail1 = m - 1, tail2 = n - 1, finished = m + n - 1;
while (tail1 >= 0 && tail2 >= 0) {
    nums1[finished--] = (nums1[tail1] > nums2[tail2]) ? 
                         nums1[tail1--] : nums2[tail2--];
}

while (tail2 >= 0) { 
    nums1[finished--] = nums2[tail2--];
}
```

## [Binary Search from Algo-Monster](https://algo.monster/problems/binary_search_intro)

Binary search is used commonly through out all interview problems, Algo-monster first introduce Vanilla-Binary Search, along with other data structure for user to get use to. The 3 I've did is: `Basic Binary Search`, `Finding the boundary`, and `First occurance of Less than k`. All of the code are pretty similar to one another.

```cpp
// Basic Binary Search
int binary_search(std::vector<int> arr, int target) {
     int left = 0;
    int right = arr.size() - 1;

    while (left <= right) { // <= here because left and right could point to the same element, < would miss it
        int mid = left + (right - left) / 2; // use `(right - left) /2` to prevent `left + right` potential overflow
        // found target, return its index
        if (arr.at(mid) == target) return mid;
        if (arr.at(mid) < target) {
            // middle less than target, discard left half by making left search boundary `mid + 1`
            left = mid + 1;
        } else {
            // middle greater than target, discard right half by making right search boundary `mid - 1`
            right = mid - 1;
        }
    }
    return -1; // if we get here we didn't hit above return so we didn't find target
}
```

This change the script to find for the smallest number, although you could index through it.
```cpp
// Modify to account for Boundary
int first_not_smaller(std::vector<int> arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    int bound = -1;
    while (left <= right) {
        int mid = (left + right) /2;
        if (arr[mid] >= target) {
            bound = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return bound;
}
```
    
With this, we essentially check for the first element that is equal to the number, or the numbers that satisfy `<= && >` for our target value.
```cpp
int find_first_occurrence(std::vector<int> arr, int target) {
    int left = 0;
    int right = arr.size() - 1;
    int firstOccurence = -1;
    while (left <= right) {
        int mid = (left + right) / 2;
        
        if (arr[mid] == target) {
            firstOccurence = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return firstOccurence;
}
```

This is the binary search for finding the first number of the square root of a given input:
```cpp
int square_root(int n) {
    int left = 0; 
    int right = n;
    int bound = 0;
    while (left <= right) {
        int mid = (left + right) / 2;
        if (mid * mid > n) {
            bound = mid;
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    return bound - 1;
}
```

## Lesson Learned
### Sliding Window / Two pointer
The pointer could be virtually anywhere; think where it'll make the most sense. Most of the two pointer questions are easy to recognized, but there are tricky parts, and algorithms. One LeetCode question was too hard to solve for me currently [Cicular Array Loop](https://leetcode.com/problems/circular-array-loop/). This is another two pointer problem, but there are multiple ways of solving it.
### Binary Search
For binary search, interpret everything as a true or false statement in which we can then traverse through. For example the first occurance could be `arr[mid] == num` or it could even be the same for the binary cases: `mid * mid > n`.
