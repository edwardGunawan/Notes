# KMP Matching Algorithm:

### Useful links: [KMP](https://www.youtube.com/watch?v=GTJr8OvyEVQ)

- Usually string matching complexity:O(mn)
- KMP string matching complexity: O(m+n)

- Basic idea: detect a mismatch (after some matchs), we already know some of the 
characters in the text of the next window.

Ex:
text: "AAAAABAAABA"
pat : "AAAA"       

- We compare first window of text with pat, we find match( same with Naive)
- but in KMP, you don't compare all over the pat again, instead,
you will know that the pattern in pat has a pattern, so you will not need 
to compare the entire pat again. 

- Need some sort propecessing to check the pat string itself has a pattern,
Ex: AAA is a patern of 123, but ABC doesn't have any pattern. We create a preprocessing
lps[] array to tells us count of character to be skipped.

**Key idea** : create a lps string that check the pat to count for the amount of 
pattern is there. 
 - Check if the pattern (smaller than the window text) if there is a suffix
 which is also a prefix. If size all character is unique then there will be none.

 How to compute if suffix = prefix?
 
 a b c d a b c a

 - make two counter i, j, where i will keep comparing between the two 
 character int he string, and j will be the counter that is compared with.
 - the value of lps[] will also be the value where the substring starts at first.
 **the value store the position on the last index that is the same in the pattern**
 - so if i and j are the same --> increment the **index** of j by 1
 - If fount mismatch, you will go to the previous j-1 index and the value of it,
 until it match, then increment that value by 1.
 - the value will serve as the position of where they string need to start to compare 
 it again.

 - Complexity: O(n) space O(n)

 - You use the preprocess array to the string, when comparing the string & substring,
 whenever find a mismatch, you will decrement the previous position, and get the value of that index

 - If there is laready a pattern when mayching, that means we can assume that
 the string do match on the previously and start with the one that doesn't match.
