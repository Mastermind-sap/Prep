<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 946. Smallest Range II

</h>
</div>

<h2><a href="https://leetcode.com/problems/smallest-range-ii" target = "_blank">946. Smallest Range II</a></h2><h3>Medium</h3><hr><p>You are given an integer array <code>nums</code> and an integer <code>k</code>.</p>

<p>For each index <code>i</code> where <code>0 &lt;= i &lt; nums.length</code>, change <code>nums[i]</code> to be either <code>nums[i] + k</code> or <code>nums[i] - k</code>.</p>

<p>The <strong>score</strong> of <code>nums</code> is the difference between the maximum and minimum elements in <code>nums</code>.</p>

<p>Return <em>the minimum <strong>score</strong> of </em><code>nums</code><em> after changing the values at each index</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [1], k = 0
<strong>Output:</strong> 0
<strong>Explanation:</strong> The score is max(nums) - min(nums) = 1 - 1 = 0.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [0,10], k = 2
<strong>Output:</strong> 6
<strong>Explanation:</strong> Change nums to be [2, 8]. The score is max(nums) - min(nums) = 8 - 2 = 6.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> nums = [1,3,6], k = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> Change nums to be [4, 6, 3]. The score is max(nums) - min(nums) = 6 - 3 = 3.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= k &lt;= 10<sup>4</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    public int smallestRangeII(int[] nums, int k) {
        int n = nums.length;
        Arrays.sort(nums);
        int maxi = nums[n - 1], mini = nums[0], res = maxi - mini;
        for (int i = 0; i < n - 1; i++) {
            maxi = Math.max(maxi, nums[i] + 2 * k);
            mini = Math.min(nums[i + 1], nums[0] + 2 * k);
            res = Math.min(res, maxi - mini);
        }
        return res;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    int smallestRangeII(vector<int>& nums, int k) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        int maxi = nums[n - 1];
        int mini = nums[0];
        int res = maxi - mini;
        for (int i = 0; i < n - 1; i++) {
            int high = max(maxi, nums[i] + 2 * k);
            int low  = min(nums[i + 1], nums[0] + 2 * k);
            res = min(res, high - low);
        }
        return res;
    }
};
```

</template>

</CodeTabs>
