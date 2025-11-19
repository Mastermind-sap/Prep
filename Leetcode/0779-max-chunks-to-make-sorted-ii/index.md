<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 779. Max Chunks To Make Sorted II

</h>
</div>

<h2><a href="https://leetcode.com/problems/max-chunks-to-make-sorted-ii" target = "_blank">779. Max Chunks To Make Sorted II</a></h2><h3>Hard</h3><hr><p>You are given an integer array <code>arr</code>.</p>

<p>We split <code>arr</code> into some number of <strong>chunks</strong> (i.e., partitions), and individually sort each chunk. After concatenating them, the result should equal the sorted array.</p>

<p>Return <em>the largest number of chunks we can make to sort the array</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [5,4,3,2,1]
<strong>Output:</strong> 1
<strong>Explanation:</strong>
Splitting into two or more chunks will not return the required result.
For example, splitting into [5, 4], [3, 2, 1] will result in [4, 5, 1, 2, 3], which isn&#39;t sorted.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,1,3,4,4]
<strong>Output:</strong> 4
<strong>Explanation:</strong>
We can split into two chunks, such as [2, 1], [3, 4, 4].
However, splitting into [2, 1], [3], [4], [4] is the highest number of chunks possible.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 2000</code></li>
	<li><code>0 &lt;= arr[i] &lt;= 10<sup>8</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    public int maxChunksToSorted(int[] arr) {
        int n = arr.length;
        int count = 0, maxi = Integer.MIN_VALUE;
        Stack<Integer> st = new Stack<>();
        for (int i = 0; i < n; i++) {
            maxi = Math.max(maxi, arr[i]);
            while (st.size() > 0 && st.peek() > arr[i])
                st.pop();
            st.add(maxi);
        }
        return st.size();
    }
}
```

</template>

<template #cpp>

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int n = arr.size();
        int count = 0;
        int maxi = INT_MIN;
        stack<int> st;
        for (int i = 0; i < n; i++) {
            maxi = max(maxi, arr[i]);
            while (!st.empty() && st.top() > arr[i])
                st.pop();
            st.push(maxi);
        }
        return st.size();
    }
};
```

</template>

</CodeTabs>
