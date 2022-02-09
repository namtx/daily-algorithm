### Problem
[leetcode](https://leetcode.com/problems/minimum-size-subarray-sum/)

### Solution

- two pointers, prefix sum

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int min = nums.length;
        int[] prefixSum = new int[nums.length];

        for (int i = 0; i < nums.length; i++) {
            prefixSum[i] = (i == 0) ? nums[i] : prefixSum[i - 1] + nums[i];
        }

        int left = 0;
        int right = 0;
        int m;
        boolean found = false;

        while (right < nums.length) {
            while (right < nums.length) {
                if (prefixSum[right] - (left == 0 ? 0 : prefixSum[left - 1]) >= target) {
                    break;
                }
                right++;
            }

            if (right == nums.length) {
                break;
            }

            int s = prefixSum[right] - (left == 0 ? 0 : prefixSum[left - 1]);
            while (s >= target) {
                left++;
                s = s - (left == 0 ? 0 : prefixSum[left - 1]);
            }
            m = right - left + 2;
            found = true;
            min = Math.min(m, min);
        }

        return !found ? 0 : min;
    }
}
```

- Time complexity: O(n)
- Space complexity: O(n)

