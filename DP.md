# Dynamic Programming

## How to solve it?
1. Identify if it is a DP problem
    - Typically all the problems that require to maximize or minimize certain 
    quantity or counting problems that say to count the arrangements under
    certain condition or certain probability problems can be solved by using 
    DP.
    - All DP problems satisfy the overlapping subproblems property and most of
    the classic DP also satisfy the optimal substructure property. Once, we 
    observe these properties in a given problem, be sure that it can be solved
    using DP.
2. Decide a state expression with least parameter
    - state transition depends on the choice of state definition you make.
    - State: defined as the set of parameters that can uniquely identify a 
    certain position or standing in the given problem. This set of parameters 
    should be as small as possible to reduce state space. Ex: Knapsack Problem,
    we define our state by two parameters **index** and **weight**, i.e. 
    DP[index][weight]. It tell us the maximum profit it can make by taking items
    from range 0 to index having the capacity of sack to be weight.
3. Formulate state relationship
    - set the state(n) = 0,~ n the one that you want to compute on. Ex: 
    if you need to compute on the total number of ways we can form a number of 
    'N' with {1,3,5}, then state(n) means total number of arrangements to form n
    by using {1,3,5} as elements. start with total number to form 1 and so on 
    until it reached n, get the optimal solution of each sub problem to get 
    the next sub-problem.
    - First, we have the intuition that we can only use {1,3,5} to form
    a given number. Let us assume that we know the result for n= 1,2,3,4,5,6;
    so we know the result of state(n=1), state (n=2), state(n=3) , state(n=4)..
    , state(n=6). Now, we wish to know the result of the state(n=7). See, we can
    only add 1, 3 and 5. Now we can get a sume total of 7 by the following 3 ways:
    1. Adding 1 to all possible combinations of state (n=6)
    2. Adding 3 to all possible combinations of state (n=4)
    3. Adding 5 to all possible combinations of state (n=2)
    Above three cases are covering all possbile ways to form a sum total of 7;
    Therefore, we can say the result for 
    ```
    state(7) = state(6) + state(4) + state(2)
     or
    state(7) = state(7-1) + state(7-3) + state(7-5)
     In general,
    state(n) = state(n-1) + state(n-3) + state(n-5)

    so the code will be a recursive like:
    int solve(int n ){
        // base case
        if(n<0) return 0;
        if(n==0) return 1;
        return solve(n-1) + solve(n-3) + solve(n-5);
    }
    ```
4. Do tabulation ( or add memoization)
    - We need to store the state answer so that next time that state is required,
    we can directly use it from our memory.
    - adding memoization is just adding a container to store the state, make it 
    as dp to store the state
    ```
    // initialize to -1
    int dp[MAXN];

    // this function returns the number of arrangements to form 'n'
    int solve(int n){
        // base case
        if(n<0) return 0;
        if(n==0) return 1;

        // checking if already calculated
        if(dp[n] != -1) return dp[n];

        // storing the result and returning 
        reutrn dp[n] = solve(n-1) + solve(n-3) + solve(n-5);
    }
    ```
    - you can also add tabulation with iteratively


## Common things about DP:

1.  Overlapping Subproblems: it is when solution is needed again and again. In DP,
computed solutions to subproblems are sotred in a table so that these don't have
to recomputed. So DP is not sueful when there are no common overlapping subproblems.

- Memoization (Top Down): similar to recursive version with a small modification 
that it looks into a lookup table before computing solutions. We initialize a 
lookup array with all initial values as NIL. Whenever, we neeed solution to a 
subproblem, we first look into the lookup table. If precomputed value is there
then we return the value, otherwise we calculate the value and put the result
in lookup table so that it can be reused later.

- Tabulation (Bottom Up) : builds a table in bottom up fashion and returns the
last entry from table.  We are building the solutions of subproblems bottom-up.
It is iteratively usually.

- Both tabulated and memoized store the solutions of subproblems. In memoized
version, table is filled on demand while in tabulated version, starting from the 
first entry, all entries are filled one by one

2.  Optimal Substructure: optimal solution of the given problem can be obtained
by using optimal solutions of its subproblems.


- First, find a recursive solution
- Then: use the memoizaition technique to store the solution in a table(array) form.
- Final: convert the memoization into an iterative program.


