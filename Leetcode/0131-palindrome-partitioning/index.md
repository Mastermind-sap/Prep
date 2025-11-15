<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 131. Palindrome Partitioning

</h>
</div>

<h2><a href="https://leetcode.com/problems/palindrome-partitioning" target = "_blank">131. Palindrome Partitioning</a></h2><h3>Medium</h3><hr><p>Given a string <code>s</code>, partition <code>s</code> such that every <span data-keyword="substring-nonempty">substring</span> of the partition is a <span data-keyword="palindrome-string"><strong>palindrome</strong></span>. Return <em>all possible palindrome partitioning of </em><code>s</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> s = "aab"
<strong>Output:</strong> [["a","a","b"],["aa","b"]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> s = "a"
<strong>Output:</strong> [["a"]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 16</code></li>
	<li><code>s</code> contains only lowercase English letters.</li>
</ul>

<CodeTabs :languages="[
  { name: 'C++', slot: 'cpp' },
  { name: 'Java', slot: 'java' }
]">

<template #java>

```java
class Solution {
    private List<List<String >> res;
    public List<List<String >> partition(String s) {
        int n = s.length();
        res = new ArrayList<>();
        solve(0, s, new ArrayList<>());
        return res;
    }
    private void solve(int ind, String s, List<String> temp) {
        if (ind >= s.length()) {
            res.add(new ArrayList<>(temp));
            return;
        }

        for (int i = ind; i < s.length(); i++) {
            String current = s.substring(ind, i + 1);
            if (is_pallindrome(current)) {
                temp.add(current);
                solve(i + 1, s, temp);
                temp.remove(temp.size() - 1);
            }
        }
    }

    private boolean is_pallindrome(String s) {
        int low = 0, high = s.length() - 1;
        while (low <= high) {
            if (s.charAt(low) != s.charAt(high))
                return false;
            low++;
            high--;
        }
        return true;
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
    vector<vector<string>> res;

    vector<vector<string>> partition(string s) {
        res.clear();
        vector<string> temp;
        solve(0, s, temp);
        return res;
    }

private:
    void solve(int ind, string &s, vector<string> &temp) {
        if (ind >= s.length()) {
            res.push_back(temp);
            return;
        }

        for (int i = ind; i < s.length(); i++) {
            string current = s.substr(ind, i - ind + 1);
            if (is_pallindrome(current)) {
                temp.push_back(current);
                solve(i + 1, s, temp);
                temp.pop_back();
            }
        }
    }

    bool is_pallindrome(const string &s) {
        int low = 0, high = s.length() - 1;
        while (low <= high) {
            if (s[low] != s[high])
                return false;
            low++;
            high--;
        }
        return true;
    }
};

```

</template>

</CodeTabs>
