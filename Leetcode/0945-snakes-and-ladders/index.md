<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 937. Online Stock Span

</h>
</div>

## 945. Snakes and Ladders

**Difficulty:** Medium

---

You are given an `n x n` integer matrix `board` where the cells are labeled from `1` to `n²` in a [**Boustrophedon style**](https://en.wikipedia.org/wiki/Boustrophedon) starting from the bottom left of the board (i.e. `board[n - 1][0]`) and alternating direction each row.

You start on square `1` of the board. In each move, starting from square `curr`, do the following:

- Choose a destination square `next` with a label in the range `[curr + 1, min(curr + 6, n²)]`.
    - This choice simulates the result of a standard **6-sided die roll**: i.e., there are always at most 6 destinations, regardless of the size of the board.
- If `next` has a snake or ladder, you **must** move to the destination of that snake or ladder. Otherwise, you move to `next`.
- The game ends when you reach the square `n²`.

A board square on row `r` and column `c` has a snake or ladder if `board[r][c] != -1`. The destination of that snake or ladder is `board[r][c]`. Squares `1` and `n²` are not the starting points of any snake or ladder.

**Note:** You only take a snake or ladder at most once per dice roll. If the destination to a snake or ladder is the start of another snake or ladder, you do **not** follow the subsequent snake or ladder.

- For example, suppose the board is `[[-1,4],[-1,3]]`, and on the first move, your destination square is `2`. You follow the ladder to square `3`, but do **not** follow the subsequent ladder to `4`.

Return _the least number of dice rolls required to reach the square_ `n²`. _If it is not possible to reach the square, return_ `-1`.

### Example 1:

![Snakes and Ladders](https://assets.leetcode.com/uploads/2018/09/23/snakes.png)

**Input:** `board = [[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,-1,-1,-1,-1,-1],[-1,35,-1,-1,13,-1],[-1,-1,-1,-1,-1,-1],[-1,15,-1,-1,-1,-1]]`

**Output:** `4`

**Explanation:**
In the beginning, you start at square 1 (at row 5, column 0).

- You decide to move to square 2 and must take the ladder to square 15.
- You then decide to move to square 17 and must take the snake to square 13.
- You then decide to move to square 14 and must take the ladder to square 35.
- You then decide to move to square 36, ending the game.

This is the lowest possible number of moves to reach the last square, so return 4.

### Example 2:

**Input:** `board = [[-1,-1],[-1,3]]`

**Output:** `1`

### Constraints:

- `n == board.length == board[i].length`
- `2 <= n <= 20`
- `board[i][j]` is either `-1` or in the range `[1, n²]`
- The squares labeled `1` and `n²` are not the starting points of any snake or ladder.

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    public int snakesAndLadders(int[][] board) {
        int n = board.length;
        HashMap<Integer, Integer> map = new HashMap<>();
        map.put(1, 0);
        Queue<Integer> q = new LinkedList<>();
        q.add(1);
        while (!q.isEmpty()) {
            int p = q.poll();
            if (p == n * n)
                return map.get(p);
            for (int i = p + 1; i <= Math.min(p + 6, n * n); i++) {
                int next = check(i, n);
                int row = next / n, col = next % n;
                int ns = board[row][col] == -1 ? i : board[row][col];
                if (!map.containsKey(ns)) {
                    map.put(ns, map.get(p) + 1);
                    q.offer(ns);
                }
            }
        }
        return -1;
    }
    public static int check(int i, int n) {
        int q = (i - 1) / n, r = (i - 1) % n;
        int row = n - 1 - q;
        int col = row % 2 != n % 2 ? r : n - 1 - r;
        return row * n + col;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    int snakesAndLadders(vector<vector<int>>& board) {
        int n = board.size();
        unordered_map<int, int> dist;
        dist[1] = 0;
        queue<int> q;
        q.push(1);
        while (!q.empty()) {
            int p = q.front();
            q.pop();
            if (p == n * n)
                return dist[p];
            for (int i = p + 1; i <= min(p + 6, n * n); i++) {
                int pos = check(i, n);
                int row = pos / n;
                int col = pos % n;
                int nextSquare = (board[row][col] == -1 ? i : board[row][col]);
                if (!dist.count(nextSquare)) {
                    dist[nextSquare] = dist[p] + 1;
                    q.push(nextSquare);
                }
            }
        }
        return -1;
    }

    static int check(int i, int n) {
        int q = (i - 1) / n;
        int r = (i - 1) % n;
        int row = n - 1 - q;
        int col;
        // zig-zag pattern
        if (row % 2 != n % 2)
            col = r;
        else
            col = n - 1 - r;
        return row * n + col;
    }
};
```

</template>

</CodeTabs>
