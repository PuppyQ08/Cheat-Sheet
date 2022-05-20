# Cheat Sheet for the algorithm and data structure

# Dynamic Programming

## Longest Common Subsequence

Plain approach
Traverse the tree model. If it didn't work out then you must build a wrong tree.
```cpp
int lcs(string s1,string s2, int n1, int n2){
    if(n1 ==0 or n2 ==0 )
        return 0;    
    if (s1[n1-1] == s2[n2-1])
        return 1 + lcs(s1,s2,n1-1,n2-1);//no branch but proceed to only one
    else
        return max(lcs(s1,s2,n1,n2-1),lcs(s1,s2,n1-1,n2));//here we enter the tree branch
}
//Complexity O(2^(max(n1,n2))) tree recursive complexity
```
Memoization: since the state is marked by n1 and n2 which is the curr index of each string, we can use a 2D array to mark our steps. 
Generally speaking, you need to find the common part in your tree.
If you can't find it, your tree is wrong.
```cpp
vector<vector<int>> memo (s1.size()+1,s2.size()+1); // +1 is because we start with no string.
int lcs(string s1,string s2, int n1, int n2){
    if(n1 ==0 or n2 ==0 )
        return 0;    
    if(memo[n1][n2]>0) return memo[m][n];
    if (s1[n1-1] == s2[n2-1])
        memo[n1][n2] = 1 + lcs(s1,s2,n1-1,n2-1);
    else
        memo[n1][n2] = max(lcs(s1,s2,n1,n2-1),lcs(s1,s2,n1-1,n2));//here we enter the tree branch
    return memo[n1][n2];
}
```
The DP process is the same but in reverse direction.
Or you can simply do no recursion but iteration through the 2D array.
Optimization: use only 1D array.

The upper description is a basic dp problem solving process:
define the tree model(brutal force)-- add memoization along the tree -- simply focus on the memoization -- optimize on the memoization.

# Binary Tree

## Iterative BFS(queue) DFS(stack)

```cpp
queue<pair<TreeNode *, int>> q;
q.push({root,sum});//or stack
while (!q.empty()){
    auto [node, curr_sum] = q.front();//stack is top()
    q.pop();
    //blah blah
    //push
    q.push({node->left, curr_sum});
}
    
```
In python you can use list to work as stack or queue but it is kind of slow.
```python
de = [(root,curr_sum),] 
while de:
    node, curr_sum = de.pop() # for queue de.pop(0)
    #bla blah
    de.append((node.right,curr_sum-node.right.val))
```

# Pointer

good habit: always initialize the pointer to NULL
```cpp
TreeNode* temp = NULL;
```
# String

- string to int and reverse
`int num = stoi(str);`
`string str = to_string(num);`

- concatenate string
`str+"test";`

- substring (string slicing)
`string str = str1.substr(beginindex,length);`

