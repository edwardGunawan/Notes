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

## Implementation

```
/* this will be worst case for O(n) */
public class KMP {
    public static void main (String args[]){
         String str = "abcxabcdabcdabcy";
         String subString = "abcdabcy";
         boolean result = kmp(subString, str);
         System.out.println(result);
    }

    public static boolean kmp(String pattern, String s) {
        int [] lps = preproc(pattern);

        int i = 0; // for the pattern
        int j = 0; // for the s

        while(i<pattern.length() && j < s.length()){
            if(pattern.charAt(i) == s.charAt(j)){
                i++;
                j++;
            }else { // if they are not the same then get the lps to 
                // see if they are the same or not, until i is 0
                // because the lps value indicate that that means there 
                // is a match between since in pattern, there is a 
                // suffix and prefix pattern that is match
                if(i == 0){
                    j++;
                }
                else {
                    i = lps[i-1];
                }
            }
        }
        if(i < pattern.length()){
            return false;
        }else {
            return true;
        }
    }

    private static int[] preproc(String pattern){
        // setting the length of hte preproc 
        // the value will be the index of the starting suffix that is not the same
        int lps[] = new int[pattern.length()];

        int j = 0;
        int i = 1;
        lps[0] = 0; // initialized all the value

        while(i<pattern.length() && j<pattern.length()){
            // if they are the same then increment the value of the lps
            // to set the initial position of the matching suffix
            if(pattern.charAt(i) == pattern.charAt(j)){
                lps[i] = j+1; // set the lps[i] to the value of the nxt j
                i++;
                j++;
            }else {
                // if it goes to 0, then just set the current lps[i] to 0
                // for instance, if abcabd, d will be 0 since it will get 
                // push back to the initial value
                if(j==0){
                    lps[i] = 0;
                    i++; // increment to compare it to the next value to see if it is the same or not
                }else {
                    // keep decrement it until j is 0
                    // keep decrement it to the last matching suffix
                    j = lps[j-1]; // have to be careful here
                }
            }
        }

        return lps;

    }
}
```    

