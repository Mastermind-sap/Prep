<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 384. Shuffle an Array

</h>
</div>

<h2><a href="https://leetcode.com/problems/shuffle-an-array" target = "_blank">384. Shuffle an Array</a></h2><h3>Medium</h3><hr><p>Given an integer array <code>nums</code>, design an algorithm to randomly shuffle the array. All permutations of the array should be <strong>equally likely</strong> as a result of the shuffling.</p>

<p>Implement the <code>Solution</code> class:</p>

<ul>
	<li><code>Solution(int[] nums)</code> Initializes the object with the integer array <code>nums</code>.</li>
	<li><code>int[] reset()</code> Resets the array to its original configuration and returns it.</li>
	<li><code>int[] shuffle()</code> Returns a random shuffling of the array.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;Solution&quot;, &quot;shuffle&quot;, &quot;reset&quot;, &quot;shuffle&quot;]
[[[1, 2, 3]], [], [], []]
<strong>Output</strong>
[null, [3, 1, 2], [1, 2, 3], [1, 3, 2]]

<strong>Explanation</strong>
Solution solution = new Solution([1, 2, 3]);
solution.shuffle();    // Shuffle the array [1,2,3] and return its result.
                       // Any permutation of [1,2,3] must be equally likely to be returned.
                       // Example: return [3, 1, 2]
solution.reset();      // Resets the array back to its original configuration [1,2,3]. Return [1, 2, 3]
solution.shuffle();    // Returns the random shuffling of array [1,2,3]. Example: return [1, 3, 2]

</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 50</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums[i] &lt;= 10<sup>6</sup></code></li>
	<li>All the elements of <code>nums</code> are <strong>unique</strong>.</li>
	<li>At most <code>10<sup>4</sup></code> calls <strong>in total</strong> will be made to <code>reset</code> and <code>shuffle</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' },
  { name: 'Java', slot: 'java' }
]">

<template #java>

```java
class Solution {
    private int original[];
    private int shuffled[];
    public Solution(int[] nums) {
        original = new int[nums.length];
        shuffled = new int[nums.length];
        for (int i = 0; i < nums.length; i++) {
            original[i] = nums[i];
            shuffled[i] = nums[i];
        }
    }
    public int[] reset() {
        return original;
    }
    public int[] shuffle() {
        ArrayList<Integer> temp = new ArrayList<>();
        for (int ele : shuffled)
            temp.add(ele);
        Collections.shuffle(temp);
        for (int i = 0; i < temp.size(); i++)
            shuffled[i] = temp.get(i);
        return shuffled;
    }
}

/**
    Your Solution object will be instantiated and called as such:
    Solution obj = new Solution(nums);
    int[] param_1 = obj.reset();
    int[] param_2 = obj.shuffle();
*/

```

</template>

<template #cpp>

```cpp
class Solution {
private:
    vector<int> original;
    vector<int> shuffled;
public:
    Solution(vector<int>& nums) {
        original = nums;
        shuffled = nums;
    }
    vector<int> reset() {
        return original;
    }
    vector<int> shuffle() {
        for (int i = shuffled.size() - 1; i > 0; i--) {
            int j = rand() % (i + 1);
            swap(shuffled[i], shuffled[j]);
        }
        return shuffled;
    }
};

```

</template>

</CodeTabs>
