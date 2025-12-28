<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 4175. Smallest All-Ones Multiple

</h>
</div>

<h2><a href="https://leetcode.com/problems/smallest-all-ones-multiple" target = "_blank">4175. Smallest All-Ones Multiple</a></h2><h3>Medium</h3><hr><p>You are given a positive integer <code>k</code>.</p>

<p>Find the <strong>smallest</strong> integer <code>n</code> divisible by <code>k</code> that consists of <strong>only the digit 1</strong> in its decimal representation (e.g., 1, 11, 111, ...).</p>

<p>Return an integer denoting the <strong>number of digits</strong> in the decimal representation of <code>n</code>. If no such <code>n</code> exists, return <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">k = 3</span></p>

<p><strong>Output:</strong> <span class="example-io">3</span></p>

<p><strong>Explanation:</strong></p>

<p><code>n = 111</code> because 111 is divisible by 3, but 1 and 11 are not. The length of <code>n = 111</code> is 3.</p>
</div>

<p><strong class="example">Example 2:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">k = 7</span></p>

<p><strong>Output:</strong> <span class="example-io">6</span></p>

<p><strong>Explanation:</strong></p>

<p><code>n = 111111</code>. The length of <code>n = 111111</code> is 6.</p>
</div>

<p><strong class="example">Example 3:</strong></p>

<div class="example-block">
<p><strong>Input:</strong> <span class="example-io">k = 2</span></p>

<p><strong>Output:</strong> <span class="example-io">-1</span></p>

<p><strong>Explanation:</strong></p>

<p>There does not exist a valid <code>n</code> that is a multiple of 2.</p>
</div>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= k &lt;= 10<sup>5</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public int minAllOneMultiple(int k) {
        if (k % 2 == 0 || k % 5  == 0)
            return - 1;
        int res = 0;
        for (int i = 1; i <= k; i++) {
            res = (res * 10 + 1) % k;
            if (res == 0)
                return i;
        }
        return -1;
    }
}
```

</template>

<template #cpp>

```cpp
// Add your C++ solution here
```

</template>

</CodeTabs>
