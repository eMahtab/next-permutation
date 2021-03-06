# Next Permutation
## https://leetcode.com/problems/next-permutation

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.
```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```
![Next Permutation](next-permutation.JPG?raw=true "Next Permutation")

### Approach :
Here is how we can solve this problem :

1. Traversing from the right, find the first nums[i] whose value is less than nums[i+1]
e.g. [1, 2, 5, 8, 7] for this given permutation, nums[i] will be 5 (index 2)

2. Next, traversing from the right, find the first nums[j], whose value is greater than nums[i] (found in step 1)
e.g. [1, 2, 5, 8, 7] for this given permutation, nums[j] will be 7

3. Swap nums[i] and nums[j]

4. Finally reverse the array elements from index i+1 to end of the input array

# Implementation :
```java
class Solution {
    public void nextPermutation(int[] nums) {
        // Starting from right, find the first pair such that nums[i] < nums[i+1]
        // [1, 2, 5, 8, 7] for this given permutation, nums[i] will be 5 (index 2)
        int i = nums.length - 2;
        while (i >= 0 && nums[i] >= nums[i+1]) {
            i--;
        }
        // Now starting from right, find the first element, which is greater the nums[i]
        if (i >= 0) {
            int j = nums.length - 1;
            while (j >= 0 && nums[j] <= nums[i]) {
                j--;
            }
            // swap nums[i] and nums[j]
            swap(nums, i, j);
        }

        // reverse all the elements, from index i+1 to end of the array
        reverse(nums, i + 1, nums.length - 1);
    }

    private void reverse(int[] nums, int lo, int hi) {
        while (lo < hi) {
            swap(nums, lo++, hi--);
        }
    }

    private void swap(int[] nums, int i, int j) {
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

### Observations :
For a decreasing permutation e.g. e.g. [5, 4, 3, 2, 1] we will not find a nums[i] in step 1, since nums[i] < nums[i+1] will never be the case for a decreasing permutation. 

e.g. [5, 4, 3, 2, 1] so index i will become -1. Since i is less than 0, it means we don't need to swap nums[i] and nums[j]. 

And we just reverse the elements in the permutation from i+1 to end of the array, in this case 0 to end of the array. So the next permutation in this case will be [1, 2, 3, 4, 5]

# References :
1. https://www.youtube.com/watch?v=Ptc_r7DIpSE
2. https://www.youtube.com/watch?v=quAS1iydq7U
