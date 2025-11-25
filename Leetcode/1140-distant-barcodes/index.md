<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1140. Distant Barcodes

</h>
</div>

<h2><a href="https://leetcode.com/problems/distant-barcodes" target = "_blank">1140. Distant Barcodes</a></h2><h3>Medium</h3><hr><p>In a warehouse, there is a row of barcodes, where the <code>i<sup>th</sup></code> barcode is <code>barcodes[i]</code>.</p>

<p>Rearrange the barcodes so that no two adjacent barcodes are equal. You may return any answer, and it is guaranteed an answer exists.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> barcodes = [1,1,1,2,2,2]
<strong>Output:</strong> [2,1,2,1,2,1]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> barcodes = [1,1,1,1,2,2,3,3]
<strong>Output:</strong> [1,3,1,3,1,2,1,2]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= barcodes.length &lt;= 10000</code></li>
	<li><code>1 &lt;= barcodes[i] &lt;= 10000</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    static class Pair {
        int node, freq, used;
        public Pair(int node, int freq, int used) {
            this.node = node;
            this.freq = freq;
            this.used = used;
        }
        @Override
        public String toString() {
            return "(" + node + " " + freq + " " + used + ")";
        }
    }
    static class custom_sort implements Comparator<Pair> {
        @Override
        public int compare(Pair first, Pair second) {
            return Integer.compare(second.freq, first.freq);
        }
    }
    public int[] rearrangeBarcodes(int[] barcodes) {
        int n = barcodes.length;
        PriorityQueue<Pair> pq = new PriorityQueue<>(new custom_sort());
        PriorityQueue<Pair> pq1 = new PriorityQueue<>(new custom_sort());
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int ele : barcodes)
            map.put(ele, map.getOrDefault(ele, 0) + 1);
        for (Map.Entry<Integer, Integer> curr : map.entrySet()) {
            int key = curr.getKey();
            int val = curr.getValue();
            pq.offer(new Pair(key, val, 0));
        }
        int res[] = new int[n];
        int k = 0;
        while (pq.size() > 0) {
            int key = pq.peek().node;
            int freq = pq.peek().freq;
            int used = pq.peek().used;
            pq.poll();
            res[k++] = key;
            if (pq1.size() > 0)
                pq.offer(pq1.poll());
            if (freq - 1 > 0)
                pq1.offer(new Pair(key, freq - 1, 1));
        }
        return res;
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

class Solution {
public:
    struct Pair {
        int node, freq, used;
        Pair(int n, int f, int u) : node(n), freq(f), used(u) {}
    };

    struct custom_sort {
        bool operator()(const Pair& a, const Pair& b) const {
            return a.freq < b.freq;  // max-heap by freq (descending)
        }
    };

    vector<int> rearrangeBarcodes(vector<int>& barcodes) {
        int n = barcodes.size();

        priority_queue<Pair, vector<Pair>, custom_sort> pq;
        priority_queue<Pair, vector<Pair>, custom_sort> pq1;
        unordered_map<int, int> map;
        for (int ele : barcodes)
            map[ele]++;
        for (auto &curr : map) {
            int key = curr.first;
            int val = curr.second;
            pq.push(Pair(key, val, 0));
        }
        vector<int> res(n);
        int k = 0;
        while (!pq.empty()) {
            int key = pq.top().node;
            int freq = pq.top().freq;
            int used = pq.top().used;
            pq.pop();
            res[k++] = key;
            if (!pq1.empty())
                pq.push(pq1.top()), pq1.pop();
            if (freq - 1 > 0)
                pq1.push(Pair(key, freq - 1, 1));
        }
        return res;
    }
};
```

</template>

</CodeTabs>
