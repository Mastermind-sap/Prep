<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 446. Arithmetic Slices II - Subsequence

</h>
</div>

<h2><a href="https://leetcode.com/problems/arithmetic-slices-ii-subsequence" target = "_blank">446. Arithmetic Slices II - Subsequence</a></h2><h3>Hard</h3><hr><p>Given an integer array <code>nums</code>, return <em>the number of all the <strong>arithmetic subsequences</strong> of</em> <code>nums</code>.</p>

<p>A sequence of numbers is called arithmetic if it consists of <strong>at least three elements</strong> and if the difference between any two consecutive elements is the same.</p>

<ul>
	<li>For example, <code>[1, 3, 5, 7, 9]</code>, <code>[7, 7, 7, 7]</code>, and <code>[3, -1, -5, -9]</code> are arithmetic sequences.</li>
	<li>For example, <code>[1, 1, 2, 5, 7]</code> is not an arithmetic sequence.</li>
</ul>

<p>A <strong>subsequence</strong> of an array is a sequence that can be formed by removing some elements (possibly none) of the array.</p>

<ul>
	<li>For example, <code>[2,5,10]</code> is a subsequence of <code>[1,2,1,<strong><u>2</u></strong>,4,1,<u><strong>5</strong></u>,<u><strong>10</strong></u>]</code>.</li>
</ul>

<p>The test cases are generated so that the answer fits in <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums = [2,4,6,8,10]
<strong>Output:</strong> 7
<strong>Explanation:</strong> All arithmetic subsequence slices are:
[2,4,6]
[4,6,8]
[6,8,10]
[2,4,6,8]
[4,6,8,10]
[2,4,6,8,10]
[2,6,10]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums = [7,7,7,7,7]
<strong>Output:</strong> 16
<strong>Explanation:</strong> Any subsequence of this array is arithmetic.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1&nbsp; &lt;= nums.length &lt;= 1000</code></li>
	<li><code>-2<sup>31</sup> &lt;= nums[i] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public int numberOfArithmeticSlices(int[] nums) {
        int n = nums.length;
        HashMap<Long, Integer>[] dp = new HashMap[n + 1];
        int res = 0;
        for (int i = 0; i < n; i++) {
            dp[i] = new HashMap<>();
            for (int j = i - 1; j >= 0; j--) {
                long diff = (long)(nums[i] * 1L - nums[j] * 1L);
                res += dp[j].getOrDefault(diff, 0);
                dp[i].put(diff, dp[i].getOrDefault(diff, 0) + dp[j].getOrDefault(diff, 0) + 1);
            }
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
    int numberOfArithmeticSlices(vector<int>& nums) {
        int n = nums.size();
        vector<unordered_map<long long, int>> dp(n);
        long long res = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i - 1; j >= 0; j--) {
                long long diff = (long long)nums[i] - (long long)nums[j];
                int prev = dp[j].count(diff) ? dp[j][diff] : 0;
                res += prev;
                dp[i][diff] += prev + 1;
            }
        }
        return (int)res;
    }
};
```

</template>

</CodeTabs>
