<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1159. Smallest Subsequence of Distinct Characters

</h>
</div>

<h2><a href="https://leetcode.com/problems/smallest-subsequence-of-distinct-characters" target = "_blank">1159. Smallest Subsequence of Distinct Characters</a></h2><h3>Medium</h3><hr><p>Given a string <code>s</code>, return <em>the </em><span data-keyword="lexicographically-smaller-string"><em>lexicographically smallest</em></span> <span data-keyword="subsequence-string"><em>subsequence</em></span><em> of</em> <code>s</code> <em>that contains all the distinct characters of</em> <code>s</code> <em>exactly once</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;bcabc&quot;
<strong>Output:</strong> &quot;abc&quot;
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> s = &quot;cbacdcbc&quot;
<strong>Output:</strong> &quot;acdb&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
</ul>

<p>&nbsp;</p>
<strong>Note:</strong> This question is the same as 316: <a href="https://leetcode.com/problems/remove-duplicate-letters/" target="_blank">https://leetcode.com/problems/remove-duplicate-letters/</a>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public String smallestSubsequence(String s) {
        int[] lastIndex = new int[26];
        for (int i = 0; i < s.length(); i++)
            lastIndex[s.charAt(i) - 'a'] = i;
        boolean[] seen = new boolean[26];
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            int currentChar = s.charAt(i) - 'a';
            if (seen[currentChar])
                continue;
            while (!stack.isEmpty() && stack.peek() > currentChar && i < lastIndex[stack.peek()])
                seen[stack.pop()] = false;
            stack.push(currentChar);
            seen[currentChar] = true;
        }
        StringBuilder result = new StringBuilder();
        while (!stack.isEmpty())
            result.append((char)(stack.pop() + 'a'));
        return result.reverse().toString();
    }
}
```

</template>

<template #cpp>

```cpp
#include <vector>
#include <string>
#include <stack>
using namespace std;

class Solution {
public:
    string smallestSubsequence(string s) {
        int n = s.size();
        vector<int> lastIndex(26);
        for (int i = 0; i < n; i++)
            lastIndex[s[i] - 'a'] = i;
        vector<bool> seen(26, false);
        stack<int> st;
        for (int i = 0; i < n; i++) {
            int currentChar = s[i] - 'a';
            if (seen[currentChar])
                continue;
            while (!st.empty() && st.top() > currentChar && i < lastIndex[st.top()]) {
                seen[st.top()] = false;
                st.pop();
            }
            st.push(currentChar);
            seen[currentChar] = true;
        }
        string result = "";
        while (!st.empty()) {
            result.push_back(char(st.top() + 'a'));
            st.pop();
        }
        reverse(result.begin(), result.end());
        return result;
    }
};
```

</template>

</CodeTabs>
