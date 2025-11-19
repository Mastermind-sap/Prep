<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 746. Prefix and Suffix Search

</h>
</div>

<h2><a href="https://leetcode.com/problems/prefix-and-suffix-search" target = "_blank">746. Prefix and Suffix Search</a></h2><h3>Hard</h3><hr><p>Design a special dictionary that searches the words in it by a prefix and a suffix.</p>

<p>Implement the <code>WordFilter</code> class:</p>

<ul>
	<li><code>WordFilter(string[] words)</code> Initializes the object with the <code>words</code> in the dictionary.</li>
	<li><code>f(string pref, string suff)</code> Returns <em>the index of the word in the dictionary,</em> which has the prefix <code>pref</code> and the suffix <code>suff</code>. If there is more than one valid index, return <strong>the largest</strong> of them. If there is no such word in the dictionary, return <code>-1</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;WordFilter&quot;, &quot;f&quot;]
[[[&quot;apple&quot;]], [&quot;a&quot;, &quot;e&quot;]]
<strong>Output</strong>
[null, 0]
<strong>Explanation</strong>
WordFilter wordFilter = new WordFilter([&quot;apple&quot;]);
wordFilter.f(&quot;a&quot;, &quot;e&quot;); // return 0, because the word at index 0 has prefix = &quot;a&quot; and suffix = &quot;e&quot;.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= words[i].length &lt;= 7</code></li>
	<li><code>1 &lt;= pref.length, suff.length &lt;= 7</code></li>
	<li><code>words[i]</code>, <code>pref</code> and <code>suff</code> consist of lowercase English letters only.</li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to the function <code>f</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class WordFilter {
    private HashMap<String, Integer> map;
    public WordFilter(String[] words) {
        int n = words.length;
        map = new HashMap<>();
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < words[i].length(); j++) {
                String prefix = words[i].substring(0, j + 1);
                for (int k = words[i].length() - 1; k >= 0; k--) {
                    String suffix = words[i].substring(k);
                    map.put(prefix + ":" + suffix, i);
                }
            }
        }
    }
    public int f(String pref, String suff) {
        return map.getOrDefault(pref + ":" + suff, -1);
    }
}
/**
    Your WordFilter object will be instantiated and called as such:
    WordFilter obj = new WordFilter(words);
    int param_1 = obj.f(pref,suff);
*/
```

</template>

<template #cpp>

```cpp
#include <bits/stdc++.h>
using namespace std;

class WordFilter {
public:
    unordered_map<string, int> mp;
    WordFilter(vector<string>& words) {
        int n = words.size();
        for (int i = 0; i < n; i++) {
            string &w = words[i];
            int len = w.length();
            for (int j = 0; j < len; j++) {
                string prefix = w.substr(0, j + 1);
                for (int k = len - 1; k >= 0; k--) {
                    string suffix = w.substr(k);
                    mp[prefix + ":" + suffix] = i;
                }
            }
        }
    }
    int f(string pref, string suff) {
        string key = pref + ":" + suff;
        if (mp.count(key)) return mp[key];
        return -1;
    }
};
```

</template>

</CodeTabs>
