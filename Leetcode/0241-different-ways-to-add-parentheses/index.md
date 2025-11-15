<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 241. Different Ways to Add Parentheses

</h>
</div>

<h2><a href="https://leetcode.com/problems/different-ways-to-add-parentheses" target = "_blank">241. Different Ways to Add Parentheses</a></h2><h3>Medium</h3><hr><p>Given a string <code>expression</code> of numbers and operators, return <em>all possible results from computing all the different possible ways to group numbers and operators</em>. You may return the answer in <strong>any order</strong>.</p>

<p>The test cases are generated such that the output values fit in a 32-bit integer and the number of different results does not exceed <code>10<sup>4</sup></code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> expression = &quot;2-1-1&quot;
<strong>Output:</strong> [0,2]
<strong>Explanation:</strong>
((2-1)-1) = 0 
(2-(1-1)) = 2
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> expression = &quot;2*3-4*5&quot;
<strong>Output:</strong> [-34,-14,-10,-10,10]
<strong>Explanation:</strong>
(2*(3-(4*5))) = -34 
((2*3)-(4*5)) = -14 
((2*(3-4))*5) = -10 
(2*((3-4)*5)) = -10 
(((2*3)-4)*5) = 10
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= expression.length &lt;= 20</code></li>
	<li><code>expression</code> consists of digits and the operator <code>&#39;+&#39;</code>, <code>&#39;-&#39;</code>, and <code>&#39;*&#39;</code>.</li>
	<li>All the integer values in the input expression are in the range <code>[0, 99]</code>.</li>
	<li>The integer values in the input expression do not have a leading <code>&#39;-&#39;</code> or <code>&#39;+&#39;</code> denoting the sign.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' },
  { name: 'Java', slot: 'java' }
]">

<template #java>

```java
class Solution {
    public List<Integer> diffWaysToCompute(String expression) {
        return diffWaysToCompute(expression, new HashMap<>());
    }
    private List<Integer> diffWaysToCompute(String expression, Map<String, List<Integer >> map) {
        if (map.containsKey(expression)) return map.get(expression);
        ArrayList<Integer> values = new ArrayList<Integer>();
        if (!hasOperator(expression))
            values.add(Integer.parseInt(expression));
        else
            for (int i = 0; i < expression.length(); i++) {
                char symbol = expression.charAt(i);
                if (!Character.isDigit(symbol)) {
                    List<Integer> leftParts = diffWaysToCompute(expression.substring(0, i), map);
                    List<Integer> rightParts = diffWaysToCompute(expression.substring(i + 1), map);
                    for (int l : leftParts)
                        for (int r : rightParts)
                            switch (symbol) {
                            case '+' -> values.add(l + r);
                            case '-' -> values.add(l - r);
                            case '*' -> values.add(l * r);
                            }
                }
            }
        return map.compute(expression, (k, v) -> values);
    }
    private boolean hasOperator(String expression) {
        for (var i = 0; i < expression.length(); i++)
            switch (expression.charAt(i)) {
            case '+', '-', '*' -> {
                        return true;
                    }
                }
        return false;
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
    vector<int> diffWaysToCompute(string expression) {
        unordered_map<string, vector<int>> mp;
        return solve(expression, mp);
    }

private:
    vector<int> solve(const string &expression, unordered_map<string, vector<int>> &mp) {
        if (mp.count(expression))
            return mp[expression];
        vector<int> values;
        if (!hasOperator(expression)) {
            values.push_back(stoi(expression));
            mp[expression] = values;
            return values;
        }
        for (int i = 0; i < expression.length(); i++) {
            char symbol = expression[i];
            if (!isdigit(symbol)) {
                string left  = expression.substr(0, i);
                string right = expression.substr(i + 1);
                vector<int> leftParts  = solve(left, mp);
                vector<int> rightParts = solve(right, mp);
                for (int l : leftParts) {
                    for (int r : rightParts) {
                        if (symbol == '+') values.push_back(l + r);
                        else if (symbol == '-') values.push_back(l - r);
                        else if (symbol == '*') values.push_back(l * r);
                    }
                }
            }
        }
        mp[expression] = values;
        return values;
    }

    bool hasOperator(const string &expression) {
        for (char c : expression) {
            if (c == '+' || c == '-' || c == '*')
                return true;
        }
        return false;
    }
};
```

</template>

</CodeTabs>
