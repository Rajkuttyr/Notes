General Approach to Backtracking Problems in Java

    With this approach you can solve any Backtracking question

    Backtracking is a foundational technique in algorithm design where we incrementally build a solution and backtrack when a constraint is violated or a goal is met. Problems like generating subsets, permutations, or combinations often follow a common recursive template.
    Below are some of the most common LeetCode backtracking problems, along with intuitive explanations and links to the problem pages.

1. 🔢 Subsets

https://leetcode.com/problems/subsets?envType=problem-list-v2&envId=backtracking
Description:

    Generate all possible subsets (the power set) of a given list of distinct integers. At each step, choose to include or exclude the current element, exploring both paths recursively.

Backtracking Idea:

    Track the current subset and start index. For each index, either include the number or move on without it.

Code


```java
class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> subsets(int[] nums) {
        List<Integer> list=new ArrayList<>();
        generate(list,nums,0);
        return res;
    }
    public void generate(List<Integer> list,int[] nums,int index){
        if(index==nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        list.add(nums[index]);
        generate(list,nums,index+1);
        list.remove(list.size()-1);
        generate(list,nums,index+1);
    }
}
 

2. ♻ Subsets II (With Duplicates)

https://leetcode.com/problems/subsets-ii/description/?envType=problem-list-v2&envId=backtracking
Description:

    Same as Subsets, but the input array may have duplicates. You must avoid duplicate subsets in the result.

Backtracking Idea:

    Sort the array. While looping, skip elements that are the same as the previous one at the same recursive depth.

Code

class Solution {
    static void helper(int[] arr,List<List<Integer>> list,List<Integer> sub,int i){
        if(i==arr.length){
            list.add(new ArrayList<>(sub));
            return;
        }
        sub.add(arr[i]);
        helper(arr,list,sub,i+1);
        sub.remove(sub.size()-1);
        int idx=i+1;
        while(idx<arr.length&&arr[i]==arr[idx]) idx++;
        helper(arr,list,sub,idx);
    }
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> list=new ArrayList<>();
        List<Integer> sub=new ArrayList<>();
        Arrays.sort(nums);
        helper(nums,list,sub,0);
        return list;
    }
}

3. 🔁 Permutations

https://leetcode.com/problems/permutations/description/?envType=problem-list-v2&envId=backtracking
Description:

    Return all possible permutations of the given distinct integers. Each number must be used once in every permutation.

Backtracking Idea:

    Track used elements and build permutations by choosing every unused number at each level.

Code

class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> permute(int[] nums) {
        // Arrays.sort(nums);
        List<Integer> list=new ArrayList<>();
        boolean[] used=new boolean[nums.length];
        permutations(nums,used,list);
        return res;
    } 
    public void permutations(int[] nums,boolean[] used,List<Integer>list){
        if(list.size()==nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if( (i>0 && nums[i]==nums[i-1])  || (used[i]) ) continue;
            list.add(nums[i]);
            used[i]=true;
            permutations(nums,used,list);
            list.remove(list.size()-1);
            used[i]=false;
        }
    }
}
```


4. 🌀 Permutations II (With Duplicates)

https://leetcode.com/problems/permutations-ii/description/
Description:

    Return all unique permutations for a list of numbers that may contain duplicates.

Backtracking Idea:

    Sort the input. Use a boolean array to mark used elements. Skip duplicates unless the previous duplicate has already been used in the current branch.

Code

```java
class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        List<Integer> list=new ArrayList<>();
        boolean[] used=new boolean[nums.length];
        permutations(nums,used,list);
        return res;
    }
    public void permutations(int[] nums,boolean[] used,List<Integer>list){
        if(list.size()==nums.length){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if( (i>0 && nums[i]==nums[i-1]) && !used[i-1] || (used[i]) ) continue;
            list.add(nums[i]);
            used[i]=true;
            permutations(nums,used,list);
            list.remove(list.size()-1);
            used[i]=false;
        }
    }
}
```

5. ➕ Combination Sum

https://leetcode.com/problems/combination-sum/description/
Description:

    Given a list of positive integers (no duplicates) and a target number, find all unique combinations that sum to the target. You can use the same number multiple times.

Backtracking Idea:

    At each step, choose the current number and recurse with updated target. Keep the index unchanged to reuse numbers.

Code
```java 
class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        generate(0,new ArrayList<>(),candidates,target,0);
        return res;
    }
    public void generate(int index,List<Integer> curr,int[] candidates, int target,int sum){
        if(sum==target){
            res.add(new ArrayList<>(curr));
            return;
        }
        if(sum>target || index>=candidates.length) return;
        curr.add(candidates[index]);
        generate(index,curr,candidates,target,sum+candidates[index]);
        curr.remove(curr.size()-1);
        generate(index+1,curr,candidates,target,sum);
    }
}

6. ➖ Combination Sum II (Single Use, With Duplicates)

https://leetcode.com/problems/combination-sum/description/
Description:

    Similar to Combination Sum, but numbers can only be used once, and duplicates in input may exist. Avoid duplicate combinations in output.

Backtracking Idea:

    Sort the array. Skip duplicates at the same recursive level. Increment the index to avoid reusing the same number.

Code

class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<Integer> list=new ArrayList<>();
        generate(candidates,target,0,list);
        return res;
    }
    public void generate(int[] candidates, int target,int start,List<Integer> list){
        if(target<0) return;
        if(target==0){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i=start;i<candidates.length;i++){
            if(i>start && candidates[i]==candidates[i-1]) continue;
            if(candidates[i]>target) break;
            list.add(candidates[i]);
            generate(candidates,target-candidates[i],i+1,list);
            list.remove(list.size()-1);
        }
    }
}
```


7.🎯Combination Sum III

https://leetcode.com/problems/combination-sum-iii/description/
Description:

    Find all valid combinations of k distinct numbers (1 to 9) that sum up to a given target n`. Each number can be used at most once.

Backtracking Idea:

    Start from 1 and try all numbers up to 9. Track the current path and total sum. Stop exploring further if:

    the sum exceeds n, or
    the path has more than k numbers.

When the path contains exactly k numbers and sums to n, add it to the result.
Code

class Solution {
    List<List<Integer>> res=new ArrayList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        int[] nums=new int[]{1,2,3,4,5,6,7,8,9};
        generate(nums,0,k,n,new ArrayList<>(),0);
        return res;
    }
    public void generate(int[] nums,int index,int size,int target,List<Integer> list,int sum){
        if(list.size()==size && sum==target){
            res.add(new ArrayList<>(list));
            return;
        }
        if(index>=nums.length || sum>target) return;
        list.add(nums[index]);
        generate(nums,index+1,size,target,list,sum+nums[index]);
        list.remove(list.size()-1);
        generate(nums,index+1,size,target,list,sum);
    }
}

8.🚀 Combination Sum IV (DP is being used in this question)

https://leetcode.com/problems/combination-sum-iv/
🔢 Problem Type: DP + Memoization (Top-Down)
🧠 Intuition:

We are given a set of numbers, and we can reuse them unlimited times to form sequences whose sum equals the target.
But unlike Combination Sum I/II, here order matters, so [1,2] and [2,1] are different.
Approach: Backtracking + Memoization

We use recursion to try each number and explore all combinations that lead to the target.
To avoid recomputation, we memoize results using a dp[] array where dp[sum] stores the number of ways to reach target from sum.
Code

class Solution {
    int res = 0;
    public int combinationSum4(int[] nums, int target) {
        Integer[] dp = new Integer[target + 1];
        generate(nums, 0, target, new ArrayList<>(), 0, dp);
        return res;
    }

    public void generate(int[] nums, int index, int target, List<Integer> curr, int sum, Integer[] dp) {
        if (sum == target) {
            res++;
            return;
        }
        if (sum > target) return;

        if (dp[sum] != null) {
            res += dp[sum];
            return;
        }

        int before = res;
        for (int i = 0; i < nums.length; i++) {
            curr.add(nums[i]);
            generate(nums, i, target, curr, sum + nums[i], dp);
            curr.remove(curr.size() - 1);
        }
        dp[sum] = res - before;
    }
}

9.🧩 Palindrome Partitioning

https://leetcode.com/problems/palindrome-partitioning/
Description:

    Partition a string such that every substring in the partition is a palindrome. Return all possible palindrome partitions.

Backtracking Idea:

    Try all partitions from the current index. Only proceed when the substring is a palindrome. Backtrack once all splits are explored.

Code

class Solution {
    List<List<String>> res=new ArrayList<>();
    public List<List<String>> partition(String s) {
        List<String> list=new ArrayList<>();
        generate(list,s,0);
        return res;
    }
    public void generate(List<String> list,String s,int idx){
        if(idx==s.length()){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i=idx;i<s.length();i++){
            if(isPalindrome(s,idx,i)){
                list.add(s.substring(idx,i+1));
                generate(list,s,i+1);
                list.remove(list.size()-1);
            }
        }
    }
    public boolean isPalindrome(String s,int start,int end){
        while(start<end){
            if(s.charAt(end)!=s.charAt(start)) return false;
            start++;
            end--;
        }
        return true;
    }
}

10.⚙ Generate Parentheses

https://leetcode.com/problems/generate-parentheses/
Description:

    Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

🔍 Intuition

    We want to generate all valid combinations of n pairs of parentheses.
    Key constraint:
    A closing ) cannot appear before its corresponding opening (.

🔄 Approach (Backtracking)

We use a recursive backtracking approach that maintains:

    open: how many '(' we can still use
    close: how many ')' we can still use

At every step:

    We can add '(' if open > 0
    We can add ')' if close > open (to maintain validity)

Code

class Solution {
    List<String> res = new ArrayList<>();
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        generate(list, 0, 0, n);
        return res;
    }
    public void generate(List<String> list, int open, int closed, int n) {
        if (open == closed && open == n) {
            StringBuilder sb = new StringBuilder();
            for (String s : list) {
                sb.append(s);
            }
            res.add(sb.toString());
            return;
        }
        if (open < n) {
            list.add("(");
            generate(list, open + 1, closed, n);
            list.remove(list.size() - 1);
        }
        if (closed < open) {
            list.add(")");
            generate(list, open, closed + 1, n);
            list.remove(list.size() - 1);
        }
    }
}

    We’ve now wrapped up all the classic pattern-style backtracking questions like Combination Sum I–IV, Subsets, Permutations, and Generate Parentheses. These problems helped build our foundation in recursion and backtracking—thinking in terms of choices, constraints, and undoing steps (backtracking).

These are a few other standard backtracking questions.
11. 👑 N-Queens I

https://leetcode.com/problems/n-queens/
The N-Queens problem is a commonly asked backtracking question and a true test of your recursive thinking. It’s not just about generating combinations—it's about placing things in a grid while satisfying constraints.
🔍 Problem Summary

You are asked to place n queens on an n x n chessboard such that no two queens attack each other. Queens can attack vertically, horizontally, and diagonally. Your goal is to return all possible valid board configurations.
🧠 Intuition

The idea is simple:

    place one queen in each row, trying every column, and backtrack if it causes conflicts. If you reach the end (i.e., all rows are filled safely), you’ve found a valid configuration.

Let's Keep it Simple

I will try to make you understand in the easiest way possible

    The question wants us to indentify all the possible positions of queen on a n x n board.
    we just have to place the queen and when there is no place left anymore for the queen, return the board.
    It's obvious that you have to make a function to check whether queen can we placed at a particular position or not(board[i][j]).
    By safe, I mean that we have to check that no queen can attack one another.
    This will be simple as we just have to check the 8 neighbours.
    Although is our approach we are going row wise so since the row below the curr row are not yet filled there is no point in checking below neighbours of a particular position.

    Now you have a clear picture of why backtracking is being used here as we have to return all possible combinations of placement of queen onto the board, hence backtracking.

⚖ Let's Implement

    Just create an n x n matrix
    fill in wiht '.' indicating empty position.
    call out generate function(refer code).
    we have made a row pointer in our generate function which tracks wheter we are inside the board range or not.
    if(ouside) just return the board.
    Now just a use a for loop to iterate over the current row's columns

for (int col = 0; col < board[row].length; col++) {
            if (isSafe(board, row, col)) {
                board[row][col] = 'Q';
                generate(board, row + 1);
                board[row][col] = '.'; 
            }
        }

    If we've placed queens in all rows (row == n), we convert the current char[][] board to a list of strings and store it in res.
    Otherwise, for each column in the current row, we check if it's safe to place a queen.
    If it's safe, we place it, recurse to the next row, and then backtrack by removing the queen.

10. That's it ✅, Let's Code.
Code

class Solution {
    List<List<String>> res = new ArrayList<>();
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }
        generate(board, 0);
        return res;
    }
    public void generate(char[][] board, int row) {
        if (row == board.length) {
            List<String> list = new ArrayList<>();
            for (int i = 0; i < board.length; i++) {
                list.add(new String(board[i]));
            }
            res.add(list);
            return;
        }
        for (int col = 0; col < board[row].length; col++) {
            if (isSafe(board, row, col)) {
                board[row][col] = 'Q';
                generate(board, row + 1);
                board[row][col] = '.'; 
            }
        }
    }
    public boolean isSafe(char[][] board, int row, int col) {
        //top row
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') return false;
        }
        //left diagonal
        // This approach is standard, you can remember this
        int maxLeft=Math.min(row,col);
        for(int i=1;i<=maxLeft;i++){
            if(board[row-i][col-i]=='Q') return false;
        }
        int maxRight=Math.min(row,board.length-1-col);
        for(int i=1;i<=maxRight;i++){
            if(board[row-i][col+i]=='Q') return false;
        }
        return true;
    }
}