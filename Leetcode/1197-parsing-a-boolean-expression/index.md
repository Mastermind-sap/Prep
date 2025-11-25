<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 1197. Parsing A Boolean Expression

</h>
</div>

<h2><a href="https://leetcode.com/problems/parsing-a-boolean-expression" target = "_blank">1197. Parsing A Boolean Expression</a></h2><h3>Hard</h3><hr><p>A <strong>boolean expression</strong> is an expression that evaluates to either <code>true</code> or <code>false</code>. It can be in one of the following shapes:</p>

<ul>
	<li><code>&#39;t&#39;</code> that evaluates to <code>true</code>.</li>
	<li><code>&#39;f&#39;</code> that evaluates to <code>false</code>.</li>
	<li><code>&#39;!(subExpr)&#39;</code> that evaluates to <strong>the logical NOT</strong> of the inner expression <code>subExpr</code>.</li>
	<li><code>&#39;&amp;(subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>)&#39;</code> that evaluates to <strong>the logical AND</strong> of the inner expressions <code>subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub></code> where <code>n &gt;= 1</code>.</li>
	<li><code>&#39;|(subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub>)&#39;</code> that evaluates to <strong>the logical OR</strong> of the inner expressions <code>subExpr<sub>1</sub>, subExpr<sub>2</sub>, ..., subExpr<sub>n</sub></code> where <code>n &gt;= 1</code>.</li>
</ul>

<p>Given a string <code>expression</code> that represents a <strong>boolean expression</strong>, return <em>the evaluation of that expression</em>.</p>

<p>It is <strong>guaranteed</strong> that the given expression is valid and follows the given rules.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input:</strong> expression = &quot;&amp;(|(f))&quot;
<strong>Output:</strong> false
<strong>Explanation:</strong> 
First, evaluate |(f) --&gt; f. The expression is now &quot;&amp;(f)&quot;.
Then, evaluate &amp;(f) --&gt; f. The expression is now &quot;f&quot;.
Finally, return false.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre>
<strong>Input:</strong> expression = &quot;|(f,f,f,t)&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> The evaluation of (false OR false OR false OR true) is true.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre>
<strong>Input:</strong> expression = &quot;!(&amp;(f,t))&quot;
<strong>Output:</strong> true
<strong>Explanation:</strong> 
First, evaluate &amp;(f,t) --&gt; (false AND true) --&gt; false --&gt; f. The expression is now &quot;!(f)&quot;.
Then, evaluate !(f) --&gt; NOT false --&gt; true. We return true.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= expression.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li>expression[i] is one following characters: <code>&#39;(&#39;</code>, <code>&#39;)&#39;</code>, <code>&#39;&amp;&#39;</code>, <code>&#39;|&#39;</code>, <code>&#39;!&#39;</code>, <code>&#39;t&#39;</code>, <code>&#39;f&#39;</code>, and <code>&#39;,&#39;</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]">

<template #java>

```java
class Solution {
    public boolean parseBoolExpr(String s) {
        int n = s.length();
        Stack<Character> first = new Stack<>();
        Stack<Character> second = new Stack<>();
        for (int i = 0; i < n; i++) {
            char current = s.charAt(i);
            if (current == ',')
                continue;
            if (current == '&' || current == '|' || current == '!')
                second.add(current);
            else {
                if (current == ')') {
                    char todo = second.pop();
                    if (todo == '&') {
                        boolean flag = true;
                        while (first.size() > 0 && first.peek() != '(') {
                            char ch = first.pop();
                            if (ch == 'f')
                                flag = false;
                        }
                        first.pop();
                        if (flag == true)
                            first.add('t');
                        else
                            first.add('f');
                    } else if (todo == '|') {
                        boolean flag = false;
                        while (first.size() > 0 && first.peek() != '(') {
                            char ch = first.pop();
                            if (ch == 't')
                                flag = true;
                        }
                        first.pop();
                        if (flag == true)
                            first.add('t');
                        else
                            first.add('f');
                    } else if (todo == '!') {
                        char ch = first.pop();
                        first.pop();
                        if (ch == 't')
                            first.add('f');
                        else
                            first.add('t');
                    }
                } else
                    first.add(current);
            }
        }
        if (first.peek() == 't')
            return true;
        return false;
    }
}
```

</template>

<template #cpp>

```cpp
#include <stack>
#include <string>
using namespace std;

class Solution {
public:
    bool parseBoolExpr(string s) {
        int n = s.size();
        stack<char> first;
        stack<char> second;
        for (int i = 0; i < n; i++) {
            char current = s[i];
            if (current == ',')
                continue;
            if (current == '&' || current == '|' || current == '!')
                second.push(current);
            else {
                if (current == ')') {
                    char todo = second.top();
                    second.pop();
                    if (todo == '&') {
                        bool flag = true;
                        while (!first.empty() && first.top() != '(') {
                            char ch = first.top(); first.pop();
                            if (ch == 'f')
                                flag = false;
                        }
                        first.pop(); // remove '('
                        first.push(flag ? 't' : 'f');
                    }
                    else if (todo == '|') {
                        bool flag = false;
                        while (!first.empty() && first.top() != '(') {
                            char ch = first.top(); first.pop();
                            if (ch == 't')
                                flag = true;
                        }
                        first.pop(); // remove '('
                        first.push(flag ? 't' : 'f');
                    }
                    else if (todo == '!') {
                        char ch = first.top(); first.pop();
                        first.pop(); // remove '('
                        first.push(ch == 't' ? 'f' : 't');
                    }
                } else {
                    first.push(current);
                }
            }
        }
        return first.top() == 't';
    }
};
```

</template>

</CodeTabs>
