<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 739. Daily Temperatures

</h>
</div>

<h2><a href="https://leetcode.com/problems/daily-temperatures" target = "_blank">739. Daily Temperatures</a></h2><h3>Medium</h3><hr><p>Given an array of integers <code>temperatures</code> represents the daily temperatures, return <em>an array</em> <code>answer</code> <em>such that</em> <code>answer[i]</code> <em>is the number of days you have to wait after the</em> <code>i<sup>th</sup></code> <em>day to get a warmer temperature</em>. If there is no future day for which this is possible, keep <code>answer[i] == 0</code> instead.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> temperatures = [73,74,75,71,69,72,76,73]
<strong>Output:</strong> [1,1,4,2,1,1,0,0]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> temperatures = [30,40,50,60]
<strong>Output:</strong> [1,1,1,0]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> temperatures = [30,60,90]
<strong>Output:</strong> [1,1,0]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;=&nbsp;temperatures.length &lt;= 10<sup>5</sup></code></li>
	<li><code>30 &lt;=&nbsp;temperatures[i] &lt;= 100</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    static class Pair {
        int node, ind;
        public Pair(int node, int ind) {
            this.node = node;
            this.ind = ind;
        }
        @Override
        public String toString() {
            return "(" + node + " " + ind + ")";
        }
    }
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        Stack<Pair> st = new Stack<>();
        int ans[] = new int[n];
        for (int i = n - 1; i >= 0; i--) {
            int current_ele = temperatures[i];
            while (st.size() > 0 && st.peek().node <= current_ele)
                st.pop();
            if (st.size() == 0)
                ans[i] = 0;
            else
                ans[i] = st.peek().ind - i;
            st.add(new Pair(current_ele, i));
        }
        return ans;
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
    struct Pair {
        int node, ind;
        Pair(int n, int i) : node(n), ind(i) {}
    };

    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        stack<Pair> st;
        vector<int> ans(n);
        for (int i = n - 1; i >= 0; i--) {
            int current_ele = temperatures[i];
            while (!st.empty() && st.top().node <= current_ele)
                st.pop();
            if (st.empty())
                ans[i] = 0;
            else
                ans[i] = st.top().ind - i;
            st.push(Pair(current_ele, i));
        }
        return ans;
    }
};
```

</template>

</CodeTabs>
