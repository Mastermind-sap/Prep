<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 2618. Maximize the Minimum Powered City

</h>
</div>

<h2><a href="https://leetcode.com/problems/maximize-the-minimum-powered-city" target = "_blank">2618. Maximize the Minimum Powered City</a></h2><h3>Hard</h3><hr><p>You are given a <strong>0-indexed</strong> integer array <code>stations</code> of length <code>n</code>, where <code>stations[i]</code> represents the number of power stations in the <code>i<sup>th</sup></code> city.</p>

<p>Each power station can provide power to every city in a fixed <strong>range</strong>. In other words, if the range is denoted by <code>r</code>, then a power station at city <code>i</code> can provide power to all cities <code>j</code> such that <code>|i - j| &lt;= r</code> and <code>0 &lt;= i, j &lt;= n - 1</code>.</p>

<ul>
	<li>Note that <code>|x|</code> denotes <strong>absolute</strong> value. For example, <code>|7 - 5| = 2</code> and <code>|3 - 10| = 7</code>.</li>
</ul>

<p>The <strong>power</strong> of a city is the total number of power stations it is being provided power from.</p>

<p>The government has sanctioned building <code>k</code> more power stations, each of which can be built in any city, and have the same range as the pre-existing ones.</p>

<p>Given the two integers <code>r</code> and <code>k</code>, return <em>the <strong>maximum possible minimum power</strong> of a city, if the additional power stations are built optimally.</em></p>

<p><strong>Note</strong> that you can build the <code>k</code> power stations in multiple cities.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> stations = [1,2,4,5,0], r = 1, k = 2
<strong>Output:</strong> 5
<strong>Explanation:</strong> 
One of the optimal ways is to install both the power stations at city 1. 
So stations will become [1,4,4,5,0].
- City 0 is provided by 1 + 4 = 5 power stations.
- City 1 is provided by 1 + 4 + 4 = 9 power stations.
- City 2 is provided by 4 + 4 + 5 = 13 power stations.
- City 3 is provided by 5 + 4 = 9 power stations.
- City 4 is provided by 5 + 0 = 5 power stations.
So the minimum power of a city is 5.
Since it is not possible to obtain a larger power, we return 5.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> stations = [4,4,4,4], r = 0, k = 3
<strong>Output:</strong> 4
<strong>Explanation:</strong> 
It can be proved that we cannot make the minimum power of a city greater than 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == stations.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= stations[i] &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= r&nbsp;&lt;= n - 1</code></li>
	<li><code>0 &lt;= k&nbsp;&lt;= 10<sup>9</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
import java.util.HashMap;

class Solution {
    private long pref[];

    static class SegmentTree {
        private long[] tree;
        private int n;
        public SegmentTree(long[] arr) {
            n = arr.length;
            tree = new long[2 * n];
            for (int i = 0; i < n; i++)
                tree[n + i] = arr[i];
            for (int i = n - 1; i > 0; i--)
                tree[i] = tree[2 * i] + tree[2 * i + 1];
        }

        public void update(int index, long val) {
            int pos = index + n;
            tree[pos] += val;
            while (pos > 1) {
                pos /= 2;
                tree[pos] = tree[2 * pos] + tree[2 * pos + 1];
            }
        }

        public long query(int left, int right) {
            left += n;
            right += n;
            long sum = 0;
            while (left <= right) {
                if ((left & 1) == 1)
                    sum += tree[left++];
                if ((right & 1) == 0)
                    sum += tree[right--];
                left /= 2;
                right /= 2;
            }
            return sum;
        }
    }

    public long maxPower(int[] stations, int r, int k) {
        int n = stations.length;
        pref = new long[n];
        pref[0] = stations[0];
        for (int i = 1; i < n; i++)
            pref[i] = pref[i - 1] + stations[i] * 1L;

        long low = 0, high = (long)(1e12), ans = -1;
        while (low <= high) {
            long mid = low + (high - low) / 2;
            if (ok(mid, stations, r, k)) {
                ans = mid;
                low = mid + 1;
            } else
                high = mid - 1;
        }
        return ans;
    }
    private boolean ok(long target, int arr[], int r, int k) {
        int n = arr.length;
        long val[] = new long[n];
        SegmentTree st = new SegmentTree(val);
        HashMap<Integer, Long> map = new HashMap<>();
        long extra = 0;
        for (int i = 0; i < n; i++) {
            int leftIdx = Math.max(0, i - r), rightIdx = Math.min(i + r, n - 1);
            long currSum = pref[rightIdx];
            if (leftIdx - 1 >= 0)
                currSum -= pref[leftIdx - 1];
            if (currSum >= target)
                continue;
            currSum += st.query(leftIdx, rightIdx);
            if (currSum >= target)
                continue;
            extra += target - currSum;
            st.update(rightIdx, target - currSum);
        }
        return extra <= k;
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
