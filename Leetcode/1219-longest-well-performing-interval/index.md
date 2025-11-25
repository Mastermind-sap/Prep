<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1219. Longest Well-Performing Interval

</h>
</div>

<h2><a href="https://leetcode.com/problems/longest-well-performing-interval" target = "_blank">1219. Longest Well-Performing Interval</a></h2><h3>Medium</h3><hr><p>We are given <code>hours</code>, a list of the number of hours worked per day for a given employee.</p>

<p>A day is considered to be a <em>tiring day</em> if and only if the number of hours worked is (strictly) greater than <code>8</code>.</p>

<p>A <em>well-performing interval</em> is an interval of days for which the number of tiring days is strictly larger than the number of non-tiring days.</p>

<p>Return the length of the longest well-performing interval.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> hours = [9,9,6,0,6,6,9]
<strong>Output:</strong> 3
<strong>Explanation: </strong>The longest well-performing interval is [9,9,6].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> hours = [6,6,6]
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= hours.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= hours[i] &lt;= 16</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public int longestWPI(int[] hours) {
        int n = hours.length;
        HashMap<Integer, Integer> map = new HashMap<>();
        int sum = 0, ans = 0;
        for (int i = 0; i < hours.length; i++) {
            if (hours[i] <= 8)
                sum += -1;
            else
                sum += 1;
            if (sum > 0)
                ans = i + 1;
            else if (map.containsKey(sum - 1))
                ans = Math.max(ans, i - map.get(sum - 1));
            if (!map.containsKey(sum))
                map.put(sum, i);
        }
        return ans;
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <unordered_map>
using namespace std;

class Solution {
public:
    int longestWPI(vector<int>& hours) {
        int n = hours.size();
        unordered_map<int, int> map;
        int sum = 0, ans = 0;
        for (int i = 0; i < n; i++) {
            if (hours[i] <= 8)
                sum += -1;
            else
                sum += 1;
            if (sum > 0)
                ans = i + 1;
            else if (map.find(sum - 1) != map.end())
                ans = max(ans, i - map[sum - 1]);
            if (map.find(sum) == map.end())
                map[sum] = i;
        }
        return ans;
    }
};
```

</template>

</CodeTabs>
