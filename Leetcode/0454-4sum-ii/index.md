<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 454. 4Sum II

</h>
</div>

<h2><a href="https://leetcode.com/problems/4sum-ii" target = "_blank">454. 4Sum II</a></h2><h3>Medium</h3><hr><p>Given four integer arrays <code>nums1</code>, <code>nums2</code>, <code>nums3</code>, and <code>nums4</code> all of length <code>n</code>, return the number of tuples <code>(i, j, k, l)</code> such that:</p>

<ul>
	<li><code>0 &lt;= i, j, k, l &lt; n</code></li>
	<li><code>nums1[i] + nums2[j] + nums3[k] + nums4[l] == 0</code></li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [1,2], nums2 = [-2,-1], nums3 = [-1,2], nums4 = [0,2]
<strong>Output:</strong> 2
<strong>Explanation:</strong>
The two tuples are:
1. (0, 0, 0, 1) -&gt; nums1[0] + nums2[0] + nums3[0] + nums4[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -&gt; nums1[1] + nums2[1] + nums3[0] + nums4[0] = 2 + (-1) + (-1) + 0 = 0
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> nums1 = [0], nums2 = [0], nums3 = [0], nums4 = [0]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums1.length</code></li>
	<li><code>n == nums2.length</code></li>
	<li><code>n == nums3.length</code></li>
	<li><code>n == nums4.length</code></li>
	<li><code>1 &lt;= n &lt;= 200</code></li>
	<li><code>-2<sup>28</sup> &lt;= nums1[i], nums2[i], nums3[i], nums4[i] &lt;= 2<sup>28</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        int n = nums1.length, count = 0;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int ele1 : nums3) {
            for (int ele2 : nums4)
                map.put((ele1 + ele2), map.getOrDefault(ele1 + ele2, 0) + 1);
        }
        for (int ele1 : nums1) {
            for (int ele2 : nums2) {
                int req = 0 - (ele1 + ele2);
                count += map.getOrDefault(req, 0);
            }
        }
        return count;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2,
                     vector<int>& nums3, vector<int>& nums4) {
        int n = nums1.size();
        unordered_map<int, int> mp;   // sum → frequency
        int count = 0;
        // Store all sums of nums3 + nums4
        for (int a : nums3) {
            for (int b : nums4) {
                mp[a + b] += 1;
            }
        }
        // Count complementary sums from nums1 + nums2
        for (int a : nums1) {
            for (int b : nums2) {
                int req = -(a + b);
                if (mp.count(req))
                    count += mp[req];
            }
        }
        return count;
    }
};
```

</template>

</CodeTabs>
