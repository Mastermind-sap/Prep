<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 991. Array of Doubled Pairs

</h>
</div>

<h2><a href="https://leetcode.com/problems/array-of-doubled-pairs" target = "_blank">991. Array of Doubled Pairs</a></h2><h3>Medium</h3><hr><p>Given an integer array of even length <code>arr</code>, return <code>true</code><em> if it is possible to reorder </em><code>arr</code><em> such that </em><code>arr[2 * i + 1] = 2 * arr[2 * i]</code><em> for every </em><code>0 &lt;= i &lt; len(arr) / 2</code><em>, or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [3,1,3,6]
<strong>Output:</strong> false
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,1,2,6]
<strong>Output:</strong> false
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> arr = [4,-2,2,-4]
<strong>Output:</strong> true
<strong>Explanation:</strong> We can take two groups, [-2,-4] and [2,4] to form [-2,-4,2,4] or [2,4,-2,-4].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= arr.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>arr.length</code> is even.</li>
	<li><code>-10<sup>5</sup> &lt;= arr[i] &lt;= 10<sup>5</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    public boolean canReorderDoubled(int[] arr) {
        int n = arr.length;
        Arrays.sort(arr);
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int ele : arr)
            map.put(ele, map.getOrDefault(ele, 0) + 1);
        for (int ele : arr) {
            if (map.getOrDefault(ele, 0) == 0)
                continue;
            if (ele < 0 && ele % 2 != 0)
                return false;
            int y = 0;
            if (ele > 0)
                y = 2 * ele;
            else
                y = ele / 2;
            if (map.getOrDefault(y, 0) == 0)
                return false;
            map.put(ele, map.getOrDefault(ele, 0) -1);
            map.put(y, map.getOrDefault(y, 0) -1);
        }
        return true;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    bool canReorderDoubled(vector<int>& arr) {
        int n = arr.size();
        sort(arr.begin(), arr.end());

        unordered_map<int, int> freq;
        for (int x : arr)
            freq[x]++;

        for (int x : arr) {
            if (freq[x] == 0)
                continue;

            if (x < 0 && x % 2 != 0)
                return false;  // odd negative cannot be halved

            int y;
            if (x > 0)
                y = 2 * x;
            else
                y = x / 2;

            if (freq[y] == 0)
                return false;

            freq[x]--;
            freq[y]--;
        }

        return true;
    }
};
```

</template>

</CodeTabs>
