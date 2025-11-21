<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1048. Clumsy Factorial

</h>
</div>

<h2><a href="https://leetcode.com/problems/clumsy-factorial" target = "_blank">1048. Clumsy Factorial</a></h2><h3>Medium</h3><hr><p>The <strong>factorial</strong> of a positive integer <code>n</code> is the product of all positive integers less than or equal to <code>n</code>.</p>

<ul>
	<li>For example, <code>factorial(10) = 10 * 9 * 8 * 7 * 6 * 5 * 4 * 3 * 2 * 1</code>.</li>
</ul>

<p>We make a <strong>clumsy factorial</strong> using the integers in decreasing order by swapping out the multiply operations for a fixed rotation of operations with multiply <code>&#39;*&#39;</code>, divide <code>&#39;/&#39;</code>, add <code>&#39;+&#39;</code>, and subtract <code>&#39;-&#39;</code> in this order.</p>

<ul>
	<li>For example, <code>clumsy(10) = 10 * 9 / 8 + 7 - 6 * 5 / 4 + 3 - 2 * 1</code>.</li>
</ul>

<p>However, these operations are still applied using the usual order of operations of arithmetic. We do all multiplication and division steps before any addition or subtraction steps, and multiplication and division steps are processed left to right.</p>

<p>Additionally, the division that we use is floor division such that <code>10 * 9 / 8 = 90 / 8 = 11</code>.</p>

<p>Given an integer <code>n</code>, return <em>the clumsy factorial of </em><code>n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> n = 4
<strong>Output:</strong> 7
<strong>Explanation:</strong> 7 = 4 * 3 / 2 + 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> n = 10
<strong>Output:</strong> 12
<strong>Explanation:</strong> 12 = 10 * 9 / 8 + 7 - 6 * 5 / 4 + 3 - 2 * 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public int clumsy(int n) {
        char operation[] = {'*', '/', '+', '-'};
        int current_operation = 0;
        ArrayList<Integer> res = new ArrayList<>();
        int current_res = n;
        for (int i = n - 1; i >= 1; i--) {
            if (operation[current_operation] == '*')
                current_res *= i;
            else if (operation[current_operation] == '/')
                current_res /= i;
            else if (operation[current_operation] == '+') {
                if (res.size() > 0)
                    current_res -= i;
                else
                    current_res += i;
            } else {
                res.add(current_res);
                current_res = i;
            }
            current_operation++;
            current_operation %= 4;
        }
        res.add(current_res);
        if (res.size() == 0)
            return current_res;
        int ans = res.get(0);
        for (int i = 1; i < res.size(); i++)
            ans -= res.get(i);
        return ans;
    }
}
```

</template>

<template #cpp>

```cpp
class Solution {
public:
    int clumsy(int n) {
        char operation[4] = {'*', '/', '+', '-'};
        int current_operation = 0;

        vector<int> res;
        int current_res = n;

        for (int i = n - 1; i >= 1; i--) {
            if (operation[current_operation] == '*') {
                current_res *= i;
            }
            else if (operation[current_operation] == '/') {
                current_res /= i;
            }
            else if (operation[current_operation] == '+') {
                if (!res.empty())
                    current_res -= i;
                else
                    current_res += i;
            }
            else { // operation '-'
                res.push_back(current_res);
                current_res = i;
            }
            current_operation = (current_operation + 1) % 4;
        }
        res.push_back(current_res);
        if (res.empty())
            return current_res;
        int ans = res[0];
        for (int i = 1; i < res.size(); i++)
            ans -= res[i];
        return ans;
    }
};
```

</template>

</CodeTabs>
