# Backtracking Programming

- Recursion is the key in backtracking programming. 
- We start with one possible move out of many available moves
and try to solve the problem if we are able to solve
the problem with the selected move, then we will print 
the solution else we will backtrack and select some other move and try 
solve it.
- If none if the moves work out we will claim that there is no solution
for the problem.
```
Generalized Algorithm:
    
    Pick a starting point.
    while(Problem is not solved)
        For each path from the starting point.
            check if selected path is safe, if yes select it
                and make recursive call to rest of the problem
             If recursive calls return true, then return true.
                else undo the urrent move and return false.
                End for
                If none of the move works out, return false, NO SOLUTION.
```


- Usually recursion base case will return to the previous code
that is run, so it will return to the previous code that run next,
so if helper() has been run and return by the base case it will 
start from the next line after helper


# DP
- A sub-solution of the problem is constructed from previously found ones.
- Polynomial complexity, which assures a much faster running time than other 
techniques like backtracking, brut-force...etc.

- Ex: Given a list of N coins, their values (V1, V2.....Vn) and the total 
sum S. Find the minimum number of coins the sum of which is S(we can use as 
many coins of one type as we want), or report that it's not possible to
select coins in such a way that they sum up to S.

- First, we need to find a state for which an optimal solution is found
and with the help of which we can find the optimal solution for the 
next state.
- What does a "state" stand for?
    * it's a way to describe a situation, a sub-solution for the problem.
    For exampe a state would be the solution for sum i, where i <= S.
    A smaller state than state i would be the solution for any sum j, where 
    j< i. For finding a state i, we need to first find all smaller states
    j (j<1). Having found the minimum number of coins which sum up to i,
    we can easily find the next state - the solution for i+1.
- How can we find it?
    


 # General approach to backtracking questions in Java (Subset, Permutation, Combination Sum, Palindrome Partitioning)

## Subset
```
    * subset that generates non duplicate set 
    public List<List<Integer>> subsets (int [] nums){
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list,new ArrayList<>(), nums,0);
        return list;
    }

    private void backtrack(List<List<Integer>> list, List<Integer>templist, int[]nums,int start){
        list.add(new ArrayList<>(tempList));
        for(int i =start; i<nums.length;i++){
            tempList.add(nums[i]);
            backtrack(list,tempList,nums,i+1);
            tempList.remove(tempList.size()-1);
        }
    }




    SubsetII (contains duplicates)
    public List<List<Integer>> subsetWithDup(int [] nums){
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list,new ArrayList<>(), nums,0);
        return list;
    }

    private void backtrack(List<List<Integer>> list , List<Integer> tempList, int[]nums,int start){
        list.add(new ArrayList<>(tempList));
        for(int i = start; i < nums.length; i++){
            if(i<start && nums[i] == nums[i-1]) continue ; // skip duplicates
            temoList.add(nums[i]);
            backtrack(list, tempList, nums, i+1);
            tempList.remove(tempList.size() - 1);
        }
    }


    Permutation
    public List<List<Integer>> permute(int [] nums){
        List<List<Integer>> list = new ArrayList<>();
       // Arrays.sort(nums); // not necessary
        backtrack(list,new ArrayList<>(), nums);
        return list;
    }
    
    private void backtrack(List<List<Integer>> list , List<Integer>tempList, int[] nums){
        if(tempList.size() == nums.length){
            list.add(new ArrayList<>(tempList));
        } else {
            for(int i = 0; i<nums.length; i++){
                if(tempList.contains(nums[i])) continue ; // element already exists
                tempList.add(nums[i]);
                backtrack(list,tempList, nums);
                tempList.remove(tempList.size() -1);
            }
        }
    }


    Permutation II (contains duplicates)
    public List<List<Integer>> permuteUnique(int [] nums){
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list, new ArrayList<>(), nums, new boolean[nums.length]);
        return list;
    }

    private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[]nums, boolean[]used){
        if(tempList.size() == nums.length){
            list.add(new ArrayList<>(tempList));
        } else {
            for(int i = 0; i<nums.length; i++){
                if(used[i] || i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;
                used[i] = true;
                tempList.add(nums[i]);
                backtrack(list,tempList, nums, used);
                used[i] = false;
                tempList.remove(tempList.size() -1);
            }
        }
    }



    Combination Sum:
    public List<List<Integer>> combinationSum(int [] nums, int target){
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list,new ArrayList<>(), nums,target, 0);
        return list;
    }

    private void backtrack(List<List<Integer>> list , List<Integer> tempList, int []nums, int remain, int start){
        if(remain < 0) return;
        else if (remain == 0) list.add(new ArrayList<>(tempList));
        else {
            for( int i = start; i<nums.length; i++){
                tempList.add(nums[i]);
                backtrack(list,tempList, nums, remain-nums[i], i); // not i + 1 because we canreuse the same element
                tempList.remove(tempList.size()-1);
            }
        }
    }


    Combination Sum II :
    public List<List<Integer>> combinationSum2(int [] nums, int target){
        List<List<Integer>> list = new ArrayList<>();
        Arrays.sort(nums);
        backtrack(list, new ArrayList<>(), nums,target, 0);
        return list;
    }

    private void backtrack(List<List<Integer>> list, List<Integer> tempList, int [] nums, int remain, int start){
        if(remain < 0) return;
        else if (remain == 0) list.add(new ArrayList<>(tempList));
        else {
            for(int i = start; i<nums.length; i++){
                if(i<start && nums[i] == nums[i-1]) continue; // skip duplicate

                tempList.add(nums[i]);
                backtrack(list,tempList,nums,remain-nums[i], i+1);
                tempList.remove(tempList.size()-1);
            }
        }
    }


    Palindrome Partitioning:
    public List<List<String>> partition(String s){
        LIst<List<String>> list = new ArrayList<>();
        backtrack(list,new ArrayList<>(),s,0);
        return list;
    }

    private void backtrack(List<List<String>> list, List<String> tempList, String s, int start){
        if(start == s.length()){
            list.add(new ArrayList<>(tempList));
        }
        else {
            for(int i = start; i<s.length; i++){
                if(isPalindrom(s,start,i)){
                    tempList.add(s.substring(start,i+1));
                    backtrack(list,tempList, s, i+1);
                    tempList.remove(tempList.size()-1);
                }
            }
        }
    }

    public boolean isPalindrome(String s, int low, int high){
        while(low<high)
            if(s.charAt(low++) != s.charAt(high--)) return false;
        return true;
    }


```

