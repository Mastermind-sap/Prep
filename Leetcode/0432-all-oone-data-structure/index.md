<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 432. All O`one Data Structure

</h>
</div>

<h2><a href="https://leetcode.com/problems/all-oone-data-structure" target = "_blank">432. All O`one Data Structure</a></h2><h3>Hard</h3><hr><p>Design a data structure to store the strings&#39; count with the ability to return the strings with minimum and maximum counts.</p>

<p>Implement the <code>AllOne</code> class:</p>

<ul>
	<li><code>AllOne()</code> Initializes the object of the data structure.</li>
	<li><code>inc(String key)</code> Increments the count of the string <code>key</code> by <code>1</code>. If <code>key</code> does not exist in the data structure, insert it with count <code>1</code>.</li>
	<li><code>dec(String key)</code> Decrements the count of the string <code>key</code> by <code>1</code>. If the count of <code>key</code> is <code>0</code> after the decrement, remove it from the data structure. It is guaranteed that <code>key</code> exists in the data structure before the decrement.</li>
	<li><code>getMaxKey()</code> Returns one of the keys with the maximal count. If no element exists, return an empty string <code>&quot;&quot;</code>.</li>
	<li><code>getMinKey()</code> Returns one of the keys with the minimum count. If no element exists, return an empty string <code>&quot;&quot;</code>.</li>
</ul>

<p><strong>Note</strong> that each function must run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;AllOne&quot;, &quot;inc&quot;, &quot;inc&quot;, &quot;getMaxKey&quot;, &quot;getMinKey&quot;, &quot;inc&quot;, &quot;getMaxKey&quot;, &quot;getMinKey&quot;]
[[], [&quot;hello&quot;], [&quot;hello&quot;], [], [], [&quot;leet&quot;], [], []]
<strong>Output</strong>
[null, null, null, &quot;hello&quot;, &quot;hello&quot;, null, &quot;hello&quot;, &quot;leet&quot;]

<strong>Explanation</strong>
AllOne allOne = new AllOne();
allOne.inc(&quot;hello&quot;);
allOne.inc(&quot;hello&quot;);
allOne.getMaxKey(); // return &quot;hello&quot;
allOne.getMinKey(); // return &quot;hello&quot;
allOne.inc(&quot;leet&quot;);
allOne.getMaxKey(); // return &quot;hello&quot;
allOne.getMinKey(); // return &quot;leet&quot;
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= key.length &lt;= 10</code></li>
	<li><code>key</code> consists of lowercase English letters.</li>
	<li>It is guaranteed that for each call to <code>dec</code>, <code>key</code> is existing in the data structure.</li>
	<li>At most <code>5 * 10<sup>4</sup></code>&nbsp;calls will be made to <code>inc</code>, <code>dec</code>, <code>getMaxKey</code>, and <code>getMinKey</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
import java.util.*;
class AllOne {
    private HashMap<String, Integer> map;
    private TreeMap<Integer, HashSet<String >> freqMap;
    public AllOne() {
        map = new HashMap<>();
        freqMap = new TreeMap<>();
    }
    public void inc(String key) {
        if (map.containsKey(key)) {
            int freq = map.get(key);
            map.put(key, freq + 1);
            freqMap.get(freq).remove(key);
            if (freqMap.get(freq).isEmpty())
                freqMap.remove(freq);
            freqMap.computeIfAbsent(freq + 1, k -> new HashSet<>()).add(key);
        } else {
            map.put(key, 1);
            freqMap.computeIfAbsent(1, k -> new HashSet<>()).add(key);
        }
    }
    public void dec(String key) {
        if (!map.containsKey(key))
            return;
        int freq = map.get(key);
        if (freq == 1) {
            map.remove(key);
            freqMap.get(1).remove(key);
            if (freqMap.get(1).isEmpty())
                freqMap.remove(1);
        } else {
            map.put(key, freq - 1);
            freqMap.get(freq).remove(key);
            if (freqMap.get(freq).isEmpty())
                freqMap.remove(freq);
            freqMap.computeIfAbsent(freq - 1, k -> new HashSet<>()).add(key);
        }
    }
    public String getMaxKey() {
        if (freqMap.isEmpty())
            return "";
        return freqMap.lastEntry().getValue().iterator().next();
    }
    public String getMinKey() {
        if (freqMap.isEmpty())
            return "";
        return freqMap.firstEntry().getValue().iterator().next();
    }
}

/**
    Your AllOne object will be instantiated and called as such:
    AllOne obj = new AllOne();
    obj.inc(key);
    obj.dec(key);
    String param_3 = obj.getMaxKey();
    String param_4 = obj.getMinKey();
*/
```

</template>

<template #cpp>

```cpp
class AllOne {
private:
    unordered_map<string, int> mp;                       // key → freq
    map<int, unordered_set<string>> freqMap;             // freq → {keys}
public:
    AllOne() {}
    void inc(string key) {
        if (mp.count(key)) {
            int freq = mp[key];
            mp[key] = freq + 1;

            freqMap[freq].erase(key);
            if (freqMap[freq].empty())
                freqMap.erase(freq);

            freqMap[freq + 1].insert(key);
        } else {
            mp[key] = 1;
            freqMap[1].insert(key);
        }
    }
    void dec(string key) {
        if (!mp.count(key))
            return;
        int freq = mp[key];
        if (freq == 1) {
            mp.erase(key);
            freqMap[1].erase(key);
            if (freqMap[1].empty())
                freqMap.erase(1);
        } else {
            mp[key] = freq - 1;
            freqMap[freq].erase(key);
            if (freqMap[freq].empty())
                freqMap.erase(freq);
            freqMap[freq - 1].insert(key);
        }
    }
    string getMaxKey() {
        if (freqMap.empty())
            return "";
        return *(freqMap.rbegin()->second.begin());
    }
    string getMinKey() {
        if (freqMap.empty())
            return "";
        return *(freqMap.begin()->second.begin());
    }
};
```

</template>

</CodeTabs>
