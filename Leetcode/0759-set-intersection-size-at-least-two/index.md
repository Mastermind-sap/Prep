<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 759. Set Intersection Size At Least Two

</h>
</div>

<h2><a href="https://leetcode.com/problems/set-intersection-size-at-least-two" target = "_blank">759. Set Intersection Size At Least Two</a></h2><h3>Hard</h3><hr><p>You are given a 2D integer array <code>intervals</code> where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code> represents all the integers from <code>start<sub>i</sub></code> to <code>end<sub>i</sub></code> inclusively.</p>

<p>A <strong>containing set</strong> is an array <code>nums</code> where each interval from <code>intervals</code> has <strong>at least two</strong> integers in <code>nums</code>.</p>

<ul>
	<li>For example, if <code>intervals = [[1,3], [3,7], [8,9]]</code>, then <code>[1,2,4,7,8,9]</code> and <code>[2,3,4,8,9]</code> are <strong>containing sets</strong>.</li>
</ul>

<p>Return <em>the minimum possible size of a containing set</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> intervals = [[1,3],[3,7],[8,9]]
<strong>Output:</strong> 5
<strong>Explanation:</strong> let nums = [2, 3, 4, 8, 9].
It can be shown that there cannot be any containing array of size 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> intervals = [[1,3],[1,4],[2,5],[3,5]]
<strong>Output:</strong> 3
<strong>Explanation:</strong> let nums = [2, 3, 4].
It can be shown that there cannot be any containing array of size 2.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> intervals = [[1,2],[2,3],[2,4],[4,5]]
<strong>Output:</strong> 5
<strong>Explanation:</strong> let nums = [1, 2, 3, 4, 5].
It can be shown that there cannot be any containing array of size 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= intervals.length &lt;= 3000</code></li>
	<li><code>intervals[i].length == 2</code></li>
	<li><code>0 &lt;= start<sub>i</sub> &lt; end<sub>i</sub> &lt;= 10<sup>8</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    static class Pair {
        int start, end;
        public Pair(int start, int end) {
            this.start = start;
            this.end = end;
        }
        @Override
        public String toString() {
            return "(" + start + " " + end + ")";
        }
    }
    static class custom_sort implements Comparator<Pair> {
        @Override
        public int compare(Pair first, Pair second) {
            int op1 = Integer.compare(first.end, second.end);
            if (op1 != 0)
                return op1;
            return Integer.compare(second.start, first.start);
        }
    }
    public int intersectionSizeTwo(int[][] intervals) {
        int n = intervals.length;
        ArrayList<Pair> res = new ArrayList<>();
        for (int current[] : intervals) {
            int start = current[0], end = current[1];
            res.add(new Pair(start, end));
        }
        Collections.sort(res, new custom_sort());
        int last = res.get(0).end, slast = res.get(0).end - 1, set_size = 2;
        for (int i = 1; i < n; i++) {
            int current_start = res.get(i).start;
            int current_end = res.get(i).end;
            if (last >= current_start && slast >= current_start)
                continue;
            if (last >= current_start) {
                slast = last;
                last = current_end;
                set_size++;
            } else {
                last = current_end;
                slast = current_end - 1;
                set_size += 2;
            }
        }
        return set_size;
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
        int start, end;
        Pair(int s, int e) : start(s), end(e) {}
    };

    struct custom_sort {
        bool operator()(const Pair &first, const Pair &second) const {
            if (first.end != second.end)
                return first.end < second.end;           // sort by end ASC
            return first.start > second.start;           // tie-break: start DESC
        }
    };

    int intersectionSizeTwo(vector<vector<int>>& intervals) {
        int n = intervals.size();
        vector<Pair> res;
        res.reserve(n);
        for (auto &cur : intervals)
            res.emplace_back(cur[0], cur[1]);
        sort(res.begin(), res.end(), custom_sort());
        int last = res[0].end;
        int slast = res[0].end - 1;
        int set_size = 2;
        for (int i = 1; i < n; i++) {
            int current_start = res[i].start;
            int current_end = res[i].end;
            // Case 1: both last and slast already inside
            if (last >= current_start && slast >= current_start)
                continue;
            // Case 2: one inside, one outside
            if (last >= current_start) {
                slast = last;
                last = current_end;
                set_size++;
            }
            // Case 3: none inside → add two new points
            else {
                last = current_end;
                slast = current_end - 1;
                set_size += 2;
            }
        }
        return set_size;
    }
};
```

</template>

</CodeTabs>
