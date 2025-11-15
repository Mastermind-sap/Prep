<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 318. Maximum Product of Word Lengths

</h>
</div>

<h2><a href="https://leetcode.com/problems/maximum-product-of-word-lengths" target = "_blank">318. Maximum Product of Word Lengths</a></h2><h3>Medium</h3><hr><p>Given a string array <code>words</code>, return <em>the maximum value of</em> <code>length(word[i]) * length(word[j])</code> <em>where the two words do not share common letters</em>. If no such two words exist, return <code>0</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> words = [&quot;abcw&quot;,&quot;baz&quot;,&quot;foo&quot;,&quot;bar&quot;,&quot;xtfn&quot;,&quot;abcdef&quot;]
<strong>Output:</strong> 16
<strong>Explanation:</strong> The two words can be &quot;abcw&quot;, &quot;xtfn&quot;.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> words = [&quot;a&quot;,&quot;ab&quot;,&quot;abc&quot;,&quot;d&quot;,&quot;cd&quot;,&quot;bcd&quot;,&quot;abcd&quot;]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The two words can be &quot;ab&quot;, &quot;cd&quot;.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> words = [&quot;a&quot;,&quot;aa&quot;,&quot;aaa&quot;,&quot;aaaa&quot;]
<strong>Output:</strong> 0
<strong>Explanation:</strong> No such pair of words.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>2 &lt;= words.length &lt;= 1000</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 1000</code></li>
	<li><code>words[i]</code> consists only of lowercase English letters.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' },
  { name: 'Java', slot: 'java' }
]">

<template #java>

```java
class Solution {
    public int maxProduct(String[] words) {
        int n = words.length;
        int freq[][] = new int[n][26];
        for (int i = 0; i < n; i++) {
            String s = words[i];
            for (int j = 0; j < s.length(); j++)
                freq[i][s.charAt(j) - 'a']++;
        }
        int maxi  = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                boolean isCommon = false;
                for (int k = 0; k < 26; k++) {
                    if (freq[i][k] > 0 && freq[j][k] > 0) {
                        isCommon = true;
                        break;
                    }
                }
                if (isCommon == false)
                    maxi = Math.max(maxi, words[i].length() * words[j].length());
            }
        }
        return maxi;
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
    int maxProduct(vector<string>& words) {
        int n = words.size();
        vector<vector<int>> freq(n, vector<int>(26, 0));
        // Build frequency table
        for (int i = 0; i < n; i++) {
            for (char c : words[i]) {
                freq[i][c - 'a']++;
            }
        }
        int maxi = 0;
        // Compare each pair of words
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                bool isCommon = false;
                for (int k = 0; k < 26; k++) {
                    if (freq[i][k] > 0 && freq[j][k] > 0) {
                        isCommon = true;
                        break;
                    }
                }
                if (!isCommon) {
                    maxi = max(maxi, (int)words[i].size() * (int)words[j].size());
                }
            }
        }
        return maxi;
    }
};
```

</template>

</CodeTabs>
