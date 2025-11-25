<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1072. Next Greater Node In Linked List

</h>
</div>

<h2><a href="https://leetcode.com/problems/next-greater-node-in-linked-list" target = "_blank">1072. Next Greater Node In Linked List</a></h2><h3>Medium</h3><hr><p>You are given the <code>head</code> of a linked list with <code>n</code> nodes.</p>

<p>For each node in the list, find the value of the <strong>next greater node</strong>. That is, for each node, find the value of the first node that is next to it and has a <strong>strictly larger</strong> value than it.</p>

<p>Return an integer array <code>answer</code> where <code>answer[i]</code> is the value of the next greater node of the <code>i<sup>th</sup></code> node (<strong>1-indexed</strong>). If the <code>i<sup>th</sup></code> node does not have a next greater node, set <code>answer[i] = 0</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/08/05/linkedlistnext1.jpg" style="width: 304px; height: 133px;" />
<pre>
<strong>Input:</strong> head = [2,1,5]
<strong>Output:</strong> [5,5,0]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/08/05/linkedlistnext2.jpg" style="width: 500px; height: 113px;" />
<pre>
<strong>Input:</strong> head = [2,7,4,3,5]
<strong>Output:</strong> [7,0,5,5,0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>n</code>.</li>
	<li><code>1 &lt;= n &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>9</sup></code></li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
/**
    Definition for singly-linked list.
    public class ListNode {
       int val;
       ListNode next;
       ListNode() {}
       ListNode(int val) { this.val = val; }
       ListNode(int val, ListNode next) { this.val = val; this.next = next; }
    }
*/
class Solution {
    public int[] nextLargerNodes(ListNode head) {
        ArrayList<Integer> nodes = new ArrayList<>();
        ListNode current = head;
        while (current != null) {
            nodes.add(current.val);
            current = current.next;
        }
        Stack<Integer> st = new Stack<>();
        int res[] = new int[nodes.size()];
        for (int i = nodes.size() - 1; i >= 0; i--) {
            int curr = nodes.get(i);
            while (st.size() > 0 && st.peek() <= curr)
                st.pop();
            if (st.size() == 0)
                res[i] = 0;
            else
                res[i] = st.peek();
            st.add(curr);
        }
        return res;
    }
}
```

</template>

<template #cpp>

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    vector<int> nextLargerNodes(ListNode* head) {
        vector<int> nodes;
        ListNode* current = head;
        while (current != nullptr) {
            nodes.push_back(current->val);
            current = current->next;
        }
        int n = nodes.size();
        vector<int> res(n, 0);
        stack<int> st;
        for (int i = n - 1; i >= 0; --i) {
            int curr = nodes[i];
            while (!st.empty() && st.top() <= curr)
                st.pop();
            if (!st.empty())
                res[i] = st.top();
            else
                res[i] = 0;
            st.push(curr);
        }
        return res;
    }
};
```

</template>

</CodeTabs>
