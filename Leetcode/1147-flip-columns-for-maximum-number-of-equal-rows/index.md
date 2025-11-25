<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1147. Flip Columns For Maximum Number of Equal Rows

</h>
</div>

<h2><a href="https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows" target = "_blank">1147. Flip Columns For Maximum Number of Equal Rows</a></h2><h3>Medium</h3><hr><p>You are given an <code>m x n</code> binary matrix <code>matrix</code>.</p>

<p>You can choose any number of columns in the matrix and flip every cell in that column (i.e., Change the value of the cell from <code>0</code> to <code>1</code> or vice versa).</p>

<p>Return <em>the maximum number of rows that have all values equal after some number of flips</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> matrix = [[0,1],[1,1]]
<strong>Output:</strong> 1
<strong>Explanation:</strong> After flipping no values, 1 row has all values equal.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> matrix = [[0,1],[1,0]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> After flipping values in the first column, both rows have equal values.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> matrix = [[0,0,0],[0,0,1],[1,1,0]]
<strong>Output:</strong> 2
<strong>Explanation:</strong> After flipping values in the first two columns, the last two rows have equal values.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == matrix.length</code></li>
	<li><code>n == matrix[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 300</code></li>
	<li><code>matrix[i][j]</code> is either&nbsp;<code>0</code> or <code>1</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public int maxEqualRowsAfterFlips(int[][] matrix) {
        int n = matrix.length, m = matrix[0].length;
        HashMap<String, Integer> map = new HashMap<>();
        int res = 0;
        for (int[] row : matrix) {
            StringBuilder sb = new StringBuilder();
            for (int ele : row)
                sb.append(ele ^ row[0]);
            String s = sb.toString();
            map.put(s, map.getOrDefault(s, 0) + 1);
            res = Math.max(res, map.get(s));
        }
        return res;
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

class Solution {
public:
    int maxEqualRowsAfterFlips(vector<vector<int>>& matrix) {
        int n = matrix.size(), m = matrix[0].size();
        unordered_map<string, int> map;
        int res = 0;
        for (auto& row : matrix) {
            string s;
            s.reserve(m);
            for (int ele : row)
                s.push_back( char((ele ^ row[0]) + '0') );
            map[s]++;
            res = max(res, map[s]);
        }
        return res;
    }
};
```

</template>

</CodeTabs>
