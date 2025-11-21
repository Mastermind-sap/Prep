<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 959. 3Sum With Multiplicity

</h>
</div>

<h2><a href="https://leetcode.com/problems/3sum-with-multiplicity" target = "_blank">959. 3Sum With Multiplicity</a></h2><h3>Medium</h3><hr><p>Given an integer array <code>arr</code>, and an integer <code>target</code>, return the number of tuples <code>i, j, k</code> such that <code>i &lt; j &lt; k</code> and <code>arr[i] + arr[j] + arr[k] == target</code>.</p>

<p>As the answer can be very large, return it <strong>modulo</strong> <code>10<sup>9</sup> + 7</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> arr = [1,1,2,2,3,3,4,4,5,5], target = 8
<strong>Output:</strong> 20
<strong>Explanation: </strong>
Enumerating by the values (arr[i], arr[j], arr[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> arr = [1,1,2,2,2,2], target = 5
<strong>Output:</strong> 12
<strong>Explanation: </strong>
arr[i] = 1, arr[j] = arr[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> arr = [2,1,3], target = 6
<strong>Output:</strong> 1
<strong>Explanation:</strong> (1, 2, 3) occured one time in the array so we return 1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= arr.length &lt;= 3000</code></li>
	<li><code>0 &lt;= arr[i] &lt;= 100</code></li>
	<li><code>0 &lt;= target &lt;= 300</code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class Solution {
    static int mod = (int)(1e9 + 7);
    static long[] factorials = new long[5000];
    static long[] invFactorials = new long[5000];
    static class Tuple {
        int first, second, third;
        public Tuple(int first, int second, int third) {
            this.first = first;
            this.second = second;
            this.third = third;
        }
        @Override
        public String toString() {
            return "(" + first + " " + second + " " + third + ")";
        }
        @Override
        public boolean equals(Object obj) {
            if (this == obj)
                return true;
            if (obj == null || getClass() != obj.getClass())
                return false;
            Tuple current = (Tuple)(obj);
            return current.first == first && current.second == second && current.third == third;
        }
        @Override
        public int hashCode() {
            return Objects.hash(first, second, third);
        }
    }
    public int threeSumMulti(int[] arr, int target) {
        precompFacts();
        int n = arr.length;
        Arrays.sort(arr);
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int ele : arr)
            map.put(ele, map.getOrDefault(ele, 0) + 1);
        HashSet<Tuple> set = new HashSet<>();
        HashSet<Tuple> res = new HashSet<>();
        for (int i = 0; i < n; i++) {
            int req = target - arr[i];
            int low = i + 1, high = n - 1;
            while (low < high) {
                if (arr[low] + arr[high] == req) {
                    res.add(new Tuple(arr[i], arr[low], arr[high]));
                    low++;
                    high--;
                } else if (arr[low] + arr[high] < req)
                    low++;
                else
                    high--;
            }
        }
        long count = 0;
        for (Tuple current : res) {
            int first = current.first;
            int second = current.second;
            int third = current.third;
            if (first == second && second == third) {
                long current_count = Math.max(1, nCk(map.getOrDefault(first, 0), 3));
                count = add(count, current_count);
            } else if (first == second && second != third) {
                long current_count = map.getOrDefault(third, 0);
                current_count = mul(current_count, Math.max(1, nCk(map.getOrDefault(first, 0), 2)));
                count = add(count, current_count);
            } else if (second == third) {
                long current_count = map.getOrDefault(first, 0);
                current_count = mul(current_count, Math.max(1, nCk(map.getOrDefault(second, 0), 2)));
                count = add(count, current_count);
            } else {
                long current_count = map.getOrDefault(first, 0);
                current_count = mul(current_count, map.getOrDefault(second, 0));
                current_count = mul(current_count, map.getOrDefault(third, 0));
                count = add(count, current_count);
            }
        }
        return (int)(count);
    }
    private static void precompFacts() {
        factorials[0] = invFactorials[0] = 1;
        for (int i = 1; i < factorials.length; i++)
            factorials[i] = mul(factorials[i - 1], i);
        invFactorials[factorials.length - 1] = exp(factorials[factorials.length - 1], mod - 2);
        for (int i = invFactorials.length - 2; i >= 0; i--)
            invFactorials[i] = mul(invFactorials[i + 1], i + 1);
    }
    private static long nCk(int n, int k) {
        return mul(factorials[n], mul(invFactorials[k], invFactorials[n - k]));
    }
    private static long exp(long base, long exp) {
        if (exp == 0)
            return 1;
        long half = exp(base, exp / 2);
        if (exp % 2 == 0)
            return mul(half, half);
        return mul(half, mul(half, base));
    }
    private static long mul(long a, long b) {
        return (long)((long)((a % mod) * 1L * (b % mod)) % mod);
    }
    private static long add(long a, long b) {
        a += b;
        if (a >= mod)
            a -= mod;
        return a;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    static const int mod = 1000000007;
    static long long factorials[5000];
    static long long invFactorials[5000];

    struct Tuple {
        int first, second, third;
        Tuple(int a, int b, int c) : first(a), second(b), third(c) {}

        bool operator==(Tuple const& other) const {
            return first == other.first &&
                   second == other.second &&
                   third == other.third;
        }
    };

    struct TupleHash {
        size_t operator()(Tuple const& t) const noexcept {
            long long h1 = std::hash<int>()(t.first);
            long long h2 = std::hash<int>()(t.second);
            long long h3 = std::hash<int>()(t.third);
            return h1 ^ (h2 << 1) ^ (h3 << 2);
        }
    };

    static void precompFacts() {
        factorials[0] = invFactorials[0] = 1;
        for (int i = 1; i < 5000; i++)
            factorials[i] = mul(factorials[i - 1], i);

        invFactorials[4999] = exp(factorials[4999], mod - 2);

        for (int i = 4998; i >= 0; i--)
            invFactorials[i] = mul(invFactorials[i + 1], i + 1);
    }

    static long long nCk(int n, int k) {
        return mul(factorials[n], mul(invFactorials[k], invFactorials[n - k]));
    }

    int threeSumMulti(vector<int>& arr, int target) {
        precompFacts();
        int n = arr.size();
        sort(arr.begin(), arr.end());

        unordered_map<int, int> freq;
        for (int x : arr)
            freq[x]++;

        unordered_set<Tuple, TupleHash> result;

        for (int i = 0; i < n; i++) {
            int req = target - arr[i];
            int low = i + 1, high = n - 1;

            while (low < high) {
                int sum = arr[low] + arr[high];
                if (sum == req) {
                    result.insert(Tuple(arr[i], arr[low], arr[high]));
                    low++;
                    high--;
                } else if (sum < req)
                    low++;
                else
                    high--;
            }
        }

        long long count = 0;

        for (auto const& t : result) {
            int a = t.first, b = t.second, c = t.third;

            if (a == b && b == c) {
                count = add(count, nCk(freq[a], 3));
            }
            else if (a == b && b != c) {
                long long cur = mul(nCk(freq[a], 2), freq[c]);
                count = add(count, cur);
            }
            else if (b == c) {
                long long cur = mul(freq[a], nCk(freq[b], 2));
                count = add(count, cur);
            }
            else {
                long long cur = mul(freq[a], mul(freq[b], freq[c]));
                count = add(count, cur);
            }
        }

        return (int)count;
    }

private:
    static long long exp(long long base, long long e) {
        if (e == 0)
            return 1;
        long long half = exp(base, e / 2);
        long long res = mul(half, half);
        if (e & 1)
            res = mul(res, base);
        return res;
    }

    static long long mul(long long a, long long b) {
        return (a % mod) * (b % mod) % mod;
    }

    static long long add(long long a, long long b) {
        a += b;
        if (a >= mod)
            a -= mod;
        return a;
    }
};

// Static array definitions
long long Solution::factorials[5000];
long long Solution::invFactorials[5000];

```

</template>

</CodeTabs>
