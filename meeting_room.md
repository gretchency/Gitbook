# Meeting Room
tags: PriorityQueue

Given an array of meeting time intervals consisting of start and end times [[s1,e1],[s2,e2],...] (si < ei), find the minimum number of conference rooms required.

```
For example,
Given [[0, 30],[5, 10],[15, 20]],
return 2.
```

利用最小堆将能合并的开会时间合并到一个屋子，计算需要几个屋子

```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
public class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        //O(nlog(n)) + O(nlog(n))
        if (intervals == null || intervals.length == 0) return 0;
        
        //Group those non-overlapping intervals into the same room, and count how many rooms needed
        
        
        //sort based on start time first
        Arrays.sort(intervals, new Comparator<Interval>(){
            @Override
            public int compare(Interval i1, Interval i2) {
                return i1.start - i2.start;
            }
        });
        
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        pq.offer(intervals[0].end);
        
        int minRooms = 1;
        for (int i = 1; i < intervals.length; i++) {
            //总是先和最小的比，看能不能凑一起
            if (intervals[i].start < pq.peek()) {
                minRooms++;
            } else {
                //说明可以挤一个房，那么先前的end就没用了
                pq.poll();
            }
            
            //无论怎样都要把比的end存进heap,因为根据这个end要么就是新开房，要么就是要等它开完会
            pq.offer(intervals[i].end);
        }
        
        return minRooms;
    }
}
```