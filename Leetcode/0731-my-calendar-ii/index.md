<div align = "center">
<h style = "margin-bottom: 0px; margin-top: 0px; color : purple;" align = "center" class = "header">

## ⌨ 731. My Calendar II

</h>
</div>

<h2><a href="https://leetcode.com/problems/my-calendar-ii" target = "_blank">731. My Calendar II</a></h2><h3>Medium</h3><hr><p>You are implementing a program to use as your calendar. We can add a new event if adding the event will not cause a <strong>triple booking</strong>.</p>

<p>A <strong>triple booking</strong> happens when three events have some non-empty intersection (i.e., some moment is common to all the three events.).</p>

<p>The event can be represented as a pair of integers <code>start</code> and <code>end</code> that represents a booking on the half-open interval <code>[start, end)</code>, the range of real numbers <code>x</code> such that <code>start &lt;= x &lt; end</code>.</p>

<p>Implement the <code>MyCalendarTwo</code> class:</p>

<ul>
	<li><code>MyCalendarTwo()</code> Initializes the calendar object.</li>
	<li><code>boolean book(int start, int end)</code> Returns <code>true</code> if the event can be added to the calendar successfully without causing a <strong>triple booking</strong>. Otherwise, return <code>false</code> and do not add the event to the calendar.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre>
<strong>Input</strong>
[&quot;MyCalendarTwo&quot;, &quot;book&quot;, &quot;book&quot;, &quot;book&quot;, &quot;book&quot;, &quot;book&quot;, &quot;book&quot;]
[[], [10, 20], [50, 60], [10, 40], [5, 15], [5, 10], [25, 55]]
<strong>Output</strong>
[null, true, true, true, false, true, true]

<strong>Explanation</strong>
MyCalendarTwo myCalendarTwo = new MyCalendarTwo();
myCalendarTwo.book(10, 20); // return True, The event can be booked. 
myCalendarTwo.book(50, 60); // return True, The event can be booked. 
myCalendarTwo.book(10, 40); // return True, The event can be double booked. 
myCalendarTwo.book(5, 15);  // return False, The event cannot be booked, because it would result in a triple booking.
myCalendarTwo.book(5, 10); // return True, The event can be booked, as it does not use time 10 which is already double booked.
myCalendarTwo.book(25, 55); // return True, The event can be booked, as the time in [25, 40) will be double booked with the third event, the time [40, 50) will be single booked, and the time [50, 55) will be double booked with the second event.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= start &lt; end &lt;= 10<sup>9</sup></code></li>
	<li>At most <code>1000</code> calls will be made to <code>book</code>.</li>
</ul>

<CodeTabs :languages="[ { name: 'C++', slot: 'cpp' }, { name: 'Java', slot: 'java' } ]"> <template #java>

```java
class MyCalendarTwo {
    private TreeMap<Integer, Integer> bookings;
    public MyCalendarTwo() {
        bookings = new TreeMap<>();
    }
    public boolean book(int start, int end) {
        bookings.put(start, bookings.getOrDefault(start, 0) + 1);
        bookings.put(end, bookings.getOrDefault(end, 0) - 1);
        int cnt = 0;
        for (int count : bookings.values()) {
            cnt += count;
            if (cnt >= 3) {
                bookings.put(start, bookings.get(start) - 1);
                if (bookings.get(start) == 0)
                    bookings.remove(start);
                bookings.put(end, bookings.get(end) + 1);
                if (bookings.get(end) == 0)
                    bookings.remove(end);
                return false;
            }
        }
        return true;
    }
}

/**
    Your MyCalendarTwo object will be instantiated and called as such:
    MyCalendarTwo obj = new MyCalendarTwo();
    boolean param_1 = obj.book(start,end);
*/
```

</template>

<template #cpp>

```cpp
#include <bits/stdc++.h>
using namespace std;

class MyCalendarTwo {
public:
    map<int, int> bookings;

    MyCalendarTwo() {}

    bool book(int start, int end) {
        // Add +1 at start and -1 at end
        bookings[start]++;
        bookings[end]--;
        int cnt = 0;
        // Check if at any point count >= 3
        for (auto &it : bookings) {
            cnt += it.second;
            if (cnt >= 3) {
                // rollback
                bookings[start]--;
                if (bookings[start] == 0)
                    bookings.erase(start);
                bookings[end]++;
                if (bookings[end] == 0)
                    bookings.erase(end);

                return false;
            }
        }
        return true;
    }
};
```

</template>

</CodeTabs>
