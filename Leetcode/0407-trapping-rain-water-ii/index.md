<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 407. Trapping Rain Water II

</h>
</div>

<h2><a href="https://leetcode.com/problems/trapping-rain-water-ii" target = "_blank">407. Trapping Rain Water II</a></h2><h3>Hard</h3><hr><p>Given an <code>m x n</code> integer matrix <code>heightMap</code> representing the height of each unit cell in a 2D elevation map, return <em>the volume of water it can trap after raining</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/08/trap1-3d.jpg" style="width: 361px; height: 321px;" />
<pre>
<strong>Input:</strong> heightMap = [[1,4,3,1,3,2],[3,2,1,3,2,4],[2,3,3,2,3,1]]
<strong>Output:</strong> 4
<strong>Explanation:</strong> After the rain, water is trapped between the blocks.
We have two small ponds 1 and 3 units trapped.
The total volume of water trapped is 4.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/04/08/trap2-3d.jpg" style="width: 401px; height: 321px;" />
<pre>
<strong>Input:</strong> heightMap = [[3,3,3,3,3],[3,2,2,2,3],[3,2,1,2,3],[3,2,2,2,3],[3,3,3,3,3]]
<strong>Output:</strong> 10
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == heightMap.length</code></li>
	<li><code>n == heightMap[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= heightMap[i][j] &lt;= 2 * 10<sup>4</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' },
  { name: 'Java', slot: 'java' }
]">

<template #java>

```java
class Solution {
    static class Pair {
        int value, row, col;
        public Pair(int value, int row, int col) {
            this.value = value;
            this.row = row;
            this.col = col;
        }
        @Override
        public String toString() {
            return "(" + value + " " + row + " " + col + ")";
        }
    }
    static class custom_sort implements Comparator<Pair> {
        @Override
        public int compare(Pair first, Pair second) {
            return Integer.compare(first.value, second.value);
        }
    }
    public int trapRainWater(int[][] arr) {
        int n = arr.length, m = arr[0].length;
        PriorityQueue<Pair> pq = new PriorityQueue<>(new custom_sort());
        int vis[][] = new int[n][m];
        for (int j = 0; j < m; j++) {
            vis[0][j] = 1;
            pq.offer(new Pair(arr[0][j], 0, j));
        }
        for (int i = 0; i < n; i++) {
            vis[i][m - 1] = 1;
            pq.offer(new Pair(arr[i][m - 1], i, m - 1));
        }
        for (int i = 0; i < n; i++) {
            vis[i][0] = 1;
            pq.offer(new Pair(arr[i][0], i, 0));
        }
        for (int j = 0; j < m; j++) {
            vis[n - 1][j] = 1;
            pq.offer(new Pair(arr[n - 1][j], n - 1, j));
        }
        int dir[][] = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        int res = 0;
        while (pq.size() > 0) {
            int cr = pq.peek().row;
            int cc = pq.peek().col;
            int cval = pq.peek().value;
            pq.poll();
            for (int dire[] : dir) {
                int nr = cr + dire[0];
                int nc = cc + dire[1];
                if (nr >= 0 && nc >= 0 && nr < n && nc < m && vis[nr][nc] == 0) {
                    vis[nr][nc] = 1;
                    res += Math.max(0, cval - arr[nr][nc]);
                    pq.offer(new Pair(Math.max(cval, arr[nr][nc]), nr, nc));
                }
            }
        }
        return res;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    struct Pair {
        int value, row, col;
        Pair(int v, int r, int c) : value(v), row(r), col(c) {}
    };
    struct custom_sort {
        bool operator()(const Pair& a, const Pair& b) const {
            return a.value > b.value;  // min-heap behavior
        }
    };
    int trapRainWater(vector<vector<int>>& arr) {
        int n = arr.size();
        int m = arr[0].size();
        priority_queue<Pair, vector<Pair>, custom_sort> pq;
        vector<vector<int>> vis(n, vector<int>(m, 0));
        for (int j = 0; j < m; j++) {
            vis[0][j] = 1;
            pq.push(Pair(arr[0][j], 0, j));
        }
        for (int i = 0; i < n; i++) {
            vis[i][m - 1] = 1;
            pq.push(Pair(arr[i][m - 1], i, m - 1));
        }
        for (int i = 0; i < n; i++) {
            vis[i][0] = 1;
            pq.push(Pair(arr[i][0], i, 0));
        }
        for (int j = 0; j < m; j++) {
            vis[n - 1][j] = 1;
            pq.push(Pair(arr[n - 1][j], n - 1, j));
        }
        int dir[4][2] = {{-1,0}, {1,0}, {0,-1}, {0,1}};
        int res = 0;
        while (!pq.empty()) {
            Pair p = pq.top();
            pq.pop();
            int cr = p.row;
            int cc = p.col;
            int cval = p.value;
            for (auto& d : dir) {
                int nr = cr + d[0];
                int nc = cc + d[1];
                if (nr >= 0 && nc >= 0 && nr < n && nc < m && vis[nr][nc] == 0) {
                    vis[nr][nc] = 1;
                    res += max(0, cval - arr[nr][nc]);
                    pq.push(Pair(max(cval, arr[nr][nc]), nr, nc));
                }
            }
        }
        return res;
    }
};
```

</template>

</CodeTabs>
