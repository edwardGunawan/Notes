# Interval Scheduling


Greedy polynomial Solution:

1. Select the interval, x, with the earliest finishing time.
2. Remove x, and all intervals intersecting x, from the set of candidate intervals.
3. Repeat until the set of candidate intervals is empty.

When ever we select an interval at step 1, we may have to remove many intervals in step 2.



Notes:

- Interval questions are questions taht give an array of two-element arrays.
The two values represent a start and an end value. Interval questions are considered to be
part of the array family but they involve some common techniques.


- Clariffy with the interviewer whether [1,2] and [2,3] are considered overlapping intervals, because it
affects how you will write your equality checks.


- Common routine for interval questions is to sort the array of intervals by 
the start value of each interval.
- Be familiar with code check if two interval overlap and to merge two overlapping intervals.

## Corner Cases
- Single interval
- Non-overlapping intervals
- An interval totally consumed within another interval
- Duplicate intervals

## Practice Questions
- [Insert Interval Leet Code Hard Questions]
- Merge Interval
- Meeting Rooms and Meeting Rooms 2
- [Non-overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/discuss/)
