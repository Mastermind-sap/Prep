<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1095. Two City Scheduling

</h>
</div>

<h2><a href="https://leetcode.com/problems/two-city-scheduling" target = "_blank">1095. Two City Scheduling</a></h2><h3>Medium</h3><hr><p>A company is planning to interview <code>2n</code> people. Given the array <code>costs</code> where <code>costs[i] = [aCost<sub>i</sub>, bCost<sub>i</sub>]</code>,&nbsp;the cost of flying the <code>i<sup>th</sup></code> person to city <code>a</code> is <code>aCost<sub>i</sub></code>, and the cost of flying the <code>i<sup>th</sup></code> person to city <code>b</code> is <code>bCost<sub>i</sub></code>.</p>

<p>Return <em>the minimum cost to fly every person to a city</em> such that exactly <code>n</code> people arrive in each city.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> costs = [[10,20],[30,200],[400,50],[30,20]]
<strong>Output:</strong> 110
<strong>Explanation: </strong>
The first person goes to city A for a cost of 10.
The second person goes to city A for a cost of 30.
The third person goes to city B for a cost of 50.
The fourth person goes to city B for a cost of 20.

The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> costs = [[259,770],[448,54],[926,667],[184,139],[840,118],[577,469]]
<strong>Output:</strong> 1859
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> costs = [[515,563],[451,713],[537,709],[343,819],[855,779],[457,60],[650,359],[631,42]]
<strong>Output:</strong> 3086
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 * n == costs.length</code></li>
	<li><code>2 &lt;= costs.length &lt;= 100</code></li>
	<li><code>costs.length</code> is even.</li>
	<li><code>1 &lt;= aCost<sub>i</sub>, bCost<sub>i</sub> &lt;= 1000</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
import java.util.Arrays;

class Solution {
    private int dp[][][];

    public int twoCitySchedCost(int[][] costs) {
        int n = costs.length;
        dp = new int[n + 1][n / 2 + 1][n / 2 + 1];
        for (int current[][] : dp)
            for (int current1[] : current)
                Arrays.fill(current1, -1);
        int res = solve(0, n / 2, n / 2, costs);
        return res;
    }

    private int solve(int ind, int aCount, int bCount, int cost[][]) {
        if (ind >= cost.length) {
            if (aCount > 0 || bCount > 0)
                return Integer.MAX_VALUE / 10;
            return 0;
        }
        if (dp[ind][aCount][bCount] != -1)
            return dp[ind][aCount][bCount];
        /* Need to decide whether to move this person to city A or B */
        int op1 = Integer.MAX_VALUE / 10, op2 = Integer.MAX_VALUE / 10;
        if (aCount > 0)
            op1 = cost[ind][0] + solve(ind + 1, aCount - 1, bCount, cost);
        if (bCount > 0)
            op2 = cost[ind][1] + solve(ind + 1, aCount, bCount - 1, cost);
        return dp[ind][aCount][bCount] = Math.min(op1, op2);
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    vector<vector<vector<int>>> dp;

    int twoCitySchedCost(vector<vector<int>>& costs) {
        int n = costs.size();
        dp = vector<vector<vector<int>>>(
            n + 1,
            vector<vector<int>>(n / 2 + 1, vector<int>(n / 2 + 1, -1))
        );
        return solve(0, n / 2, n / 2, costs);
    }

    int solve(int ind, int aCount, int bCount, vector<vector<int>>& cost) {
        if (ind >= cost.size()) {
            if (aCount > 0 || bCount > 0)
                return 1000000000;
            return 0;
        }
        if (dp[ind][aCount][bCount] != -1)
            return dp[ind][aCount][bCount];
        int op1 = 1000000000, op2 = 1000000000;
        if (aCount > 0)
            op1 = cost[ind][0] + solve(ind + 1, aCount - 1, bCount, cost);
        if (bCount > 0)
            op2 = cost[ind][1] + solve(ind + 1, aCount, bCount - 1, cost);
        return dp[ind][aCount][bCount] = min(op1, op2);
    }
};
```

</template>

</CodeTabs>
