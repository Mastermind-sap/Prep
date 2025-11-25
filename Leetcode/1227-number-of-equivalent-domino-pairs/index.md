<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1227. Number of Equivalent Domino Pairs

</h>
</div>

<h2><a href="https://leetcode.com/problems/number-of-equivalent-domino-pairs" target = "_blank">1227. Number of Equivalent Domino Pairs</a></h2><h3>Easy</h3><hr><p>Given a list of <code>dominoes</code>, <code>dominoes[i] = [a, b]</code> is <strong>equivalent to</strong> <code>dominoes[j] = [c, d]</code> if and only if either (<code>a == c</code> and <code>b == d</code>), or (<code>a == d</code> and <code>b == c</code>) - that is, one domino can be rotated to be equal to another domino.</p>

<p>Return <em>the number of pairs </em><code>(i, j)</code><em> for which </em><code>0 &lt;= i &lt; j &lt; dominoes.length</code><em>, and </em><code>dominoes[i]</code><em> is <strong>equivalent to</strong> </em><code>dominoes[j]</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> dominoes = [[1,2],[2,1],[3,4],[5,6]]
<strong>Output:</strong> 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> dominoes = [[1,2],[1,2],[1,1],[1,2],[2,2]]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= dominoes.length &lt;= 4 * 10<sup>4</sup></code></li>
	<li><code>dominoes[i].length == 2</code></li>
	<li><code>1 &lt;= dominoes[i][j] &lt;= 9</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    static class Pair {
        int first, second;
        public Pair(int first, int second) {
            this.first = first;
            this.second = second;
        }
        @Override
        public String toString() {
            return "(" + first + " " + second + ")";
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null || getClass() != obj.getClass())
                return false;
            Pair current = (Pair)(obj);
            return current.first == first && current.second == second;
        }
        @Override
        public int hashCode() {
            return Objects.hash(first, second);
        }
    }
    public int numEquivDominoPairs(int[][] arr) {
        int n = arr.length;
        HashMap<Pair, Integer> map = new HashMap<>();
        for (int i = 0; i < n; i++)
            map.put(new Pair(arr[i][0], arr[i][1]), map.getOrDefault(new Pair(arr[i][0], arr[i][1]), 0) + 1);
        int count = 0;
        for (int i = 0; i < n; i++) {
            int x = arr[i][0], y = arr[i][1];
            if (x == y) {
                count += map.getOrDefault(new Pair(x, y), 0) - 1;
                if (map.getOrDefault(new Pair(x, y), 0) > 0)
                    map.put(new Pair(x, y), map.getOrDefault(new Pair(x, y), 0) -1);
            } else {
                count += map.getOrDefault(new Pair(x, y), 0) - 1;
                count += map.getOrDefault(new Pair(y, x), 0);
                if (map.getOrDefault(new Pair(x, y), 0) > 0)
                    map.put(new Pair(x, y), map.getOrDefault(new Pair(x, y), 0) -1);
            }
        }
        return count;
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <unordered_map>
#include <functional>
using namespace std;

class Solution {
public:
    struct Pair {
        int first, second;
        Pair(int f = 0, int s = 0) : first(f), second(s) {}

        bool operator==(const Pair& other) const {
            return first == other.first && second == other.second;
        }
    };

    struct PairHash {
        size_t operator()(Pair const& p) const noexcept {
            return hash<int>()(p.first) ^ (hash<int>()(p.second) << 1);
        }
    };

    int numEquivDominoPairs(vector<vector<int>>& arr) {
        int n = arr.size();
        unordered_map<Pair, int, PairHash> map;
        for (int i = 0; i < n; i++) {
            Pair p(arr[i][0], arr[i][1]);
            map[p] = (map.count(p) ? map[p] : 0) + 1;
        }
        int count = 0;
        for (int i = 0; i < n; i++) {
            int x = arr[i][0], y = arr[i][1];
            Pair p1(x, y);
            Pair p2(y, x);
            if (x == y) {
                count += (map.count(p1) ? map[p1] : 0) - 1;
                if (map.count(p1) && map[p1] > 0)
                    map[p1] = map[p1] - 1;
            }
            else {
                count += (map.count(p1) ? map[p1] : 0) - 1;
                count += (map.count(p2) ? map[p2] : 0);

                if (map.count(p1) && map[p1] > 0)
                    map[p1] = map[p1] - 1;
            }
        }
        return count;
    }
};
```

</template>

</CodeTabs>
