# Sliding Window Algoirhtm

## Questions for Find All anagrams in a String
- Basically find all the position of the character in the string that is 
anagrams to the pattern

- Get a length of 256 int array, loop through the pattern and increment 
the count on the index of the pattern
- Create two pointer: left, right, and the count that is the length of the pattern
- loop through the string and decrement the value of the array that is created
    * if the value is less than 0 means there is no character match in the pattern
    * if the value is 0 or bigger, that means there is character match in the pattern
    * decrement the count if it exist
    * increment right pointer
- if the count is 0, then push the left to the List
- check if the right - left is 0, if it is 0, 
    * reseting the left value in the array, if the left value is less than 0
    means there is no character match, so don't increment the count
    * but if the left value in the array is 0 or greater means there is a 
    match in the cahracter so increment the count
    * increment the value and increment hte left to set the window to the same 
    size as the pattern

```
    public class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        /* creating new integer array to count for the amount of character there is in the string
            by comparing them everytime when looping, and decrementing the value in the index 
            of the string
            
            Like the sliding window, if the window gets too wide, you have to narrow down by
            increment the left pointer and reseting back the value, if the value is >0
            that means there is a match in the String p, so you increment the count to 
            reset the value */
        int [] arr = new int[256]; // 256 character in an alphabet
        List<Integer> res = new ArrayList<>();
        int left = 0, right =0, pLen = p.length(), count = p.length(); // initialized the j and i and the pLen
        for(int k = 0; k<p.length(); k++){
            arr[p.charAt(k)]++; // increment the value of all the position in the string p in arr
        }
        
        while(right<s.length()){
            if(arr[s.charAt(right)] >=1 ){ // if it is greater than 1 means there is the same character in p
                count--;
            }
            // even if p is not right it will still decrement so it will be negative later when incrementing it,
            // or checking it, if it is not greater or equal to 0, means that the s has character that doesn't
            // match with p (since we are looking for the anagrams)
            arr[s.charAt(right)]--; // count that so that if s has multiple but p has 1 that will be negative
            right++; 
            if(count == 0){
                res.add(left); // add the initial value to the res
            }
            
            if(right-left == pLen){
                if(arr[s.charAt(left)] >= 0){ // if it is equal to 0 means there is a match beacuse it is not negative
                    count++;
                }
                // reset everything back
                arr[s.charAt(left)]++;
                left++;
            }
        }
        
        return res;
        
    }
}
```

## 10- line template that can solve most 'substring' problem

- For most substring problem, we are given a string and need to find a subtring of it
which satisfy some restrictions. A general way is use a hashmap assisted with two pointers.

```
public int findSubtring(string s){
    int [] arr = new int[256];
    int counter = 0; // check whether the subtring is valid
    int begin =0, end = 0; // two pointers, one point to tail and one head
    ind d = 0; // length of the substring

    for() { /* initialized the hash map here */}

    while(end < s.length()){
        if(arr[s.charAt(end++)]-- ?){ /* modify counter here */ }

        /* this is to check if the counter is outside of its
        valid requirement of the questions, then either reset it  */
        while(/*counter condition */){
            
            /* update d here if finding minimum */

            // increase begin to make it invalid/valid again

            if(arr[s.charAt(begin++)]++ ? ) { /* modify counter here */ }
        }

        /* update d here if finding maximum */
    }

    return d;
}

note that arr[s.charAt(begin++)]-- means 
    arr[s.charAt(begin)] 
    arr[s.charAt(begin)] --;
    begin++;
 ```

 ```
 Longest Substring with At Most Two Distinct Characters

 public int lengthOfLongestSubstringTwoDistinct(string s){
    int [] arr = new int[256];
    int counter = 0, begin =0, end = 0;
    while(end < s.size()){
        // if the array value is 0 then increment the counter means the 
        // substring has not yet been there, this is to checkout 
        // if the substring that is in the requirement of the problem is valid or not
        if(arr[s.charAt(end++)]++ == 0) counter ++; 
        
        // to check the current counter if it is 2 then reset the counter back
        // finding the current substring to reset it back, since it already find
        // 2 distinct character
        while(counter > 2) if(arr[s.charAt(begin++)]-- == 1) counter--;

        // finding the maximum of the substring here
        d = Math.max(d,end-begin);
    }
    return d;
 }
 ```

 ```
 Longest Substring without repeating characters

 public int lengthOfLongestSubtringWithoutRepeatingCharacter(String s ){
     int [] arr = new int[256];
     int begin = 0, end = 0, counter = 0;
    
     while(end < s.length()){
         // this is to check if it is valid or not with the requirement
         if(arr[s.charAt(end++)]++ >0) counter++;
         
         // this is if it is outside of its more than 1 character (validity),
         // reset everything by updating the window of begin, 
         // until it is valid, and calculate the length difference
         // between end and begin after wards, and take a max out 
         // store it in d
         while(counter >0) if(arr[s.charAt(begin++)]-- >1) counter--;

         d = max(d,end-begin); // while it is valid then update the d
     }
     return d;
 }

 since substring is contiguous so everytime when it is outside of its
 validity, we have to increment the begin++ and slide back the window 
 to its valid requirement of the problem, then get the length of it 
 and compute the maximum amount of length 

 ```
