# Cheat Sheet for the algorithm and data structure
## Topic:
- Search: Backtrack/recursion, BFS/DFS, Binary search.
- sort: quick sort, merge sort...
- strategy: divide n conquer, greedy, two pointer, sliding window,prefix sum,
- Dynamic programming
- data structure: queue/stack, linked list,heap, hash table, tree, graph, union find, string


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

# Iterative BFS(queue) DFS(stack)

***use recursion is the same as using stack because recursion uses the call stack.***

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
Monotonic stacks are a good option when a problem involves comparing the size of numeric elements, with their order being relevant.

# Binary Search

The key point of Binary search is not only for finding a "target" value.
But it can be generalized to :
- To find which part does **not** have target.
- To find the boarder of searching space.

    The target is flexible:
    for example, lc 658 find K closest ele, you can use nums[mid+k] work as target to compare with nums[mid] 

Here are several possible templates:

1. left and right close.

```cpp
int binarySearch(vector<int>& nums, int target){
  if(nums.size() == 0)
    return -1;

  int left = 0, right = nums.size() - 1;
  while(left <= right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid - 1; }
  }

  // End Condition: left > right
  return -1;
}
```

2. left close and right open (if you need to determine the right element)

This is good if you need to get access to mid+1 value
left and right close algo will access out of array since mid = arry.size() you still want to get access to mid+1
But this algo:mid = size()
```cpp
int left = 0, right = nums.size();
  while(left < right){
    // Prevent (left + right) overflow
    int mid = left + (right - left) / 2;
    if(nums[mid] == target){ return mid; }
    else if(nums[mid] < target) { left = mid + 1; }
    else { right = mid; }
  }
```
here template 2 is equivalent to template 1 because you just need to compare with target.
But if you need to access to mid and mid+1 value (which is the reason we use template),
you need to change `right= nums.size()` to `right= nums.size()-1` otherwise you got segfault.

Also if the vector has duplicated numbers, and you want to find the edge of target*n, lager value.
You can simply do
```cpp
if(nums[mid]<target) l = mid+1;
else  r= mid;
return l;// but you need left
// you can also use template 1 I recommand that .
``` 
This is an alternative procedure published by Hermannin 1962. (see in Wikipedia"binary search")

3. left and right open:
This is good if you need mid-1 mid and mid+1,
```cpp
   int left = 0, right = nums.length - 1;
    while (left + 1 < right){
        // Prevent (left + right) overflow
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            return mid;
        } else if (nums[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }
```
It need post-processing: Loop/Recursion ends when you have 2 elements left. Need to assess if the remaining elements meet the condition.
So I don't recommand this template:
You can use template 1 or 2 but if you need to get access to mid-1:
simpy add: `if(mid==left || nums[mid-1] ==target)` 

# array

`array = [1,2,3,4]`

Subarray : [1,2],[1,2,3] - is continous and maintains relative order of elements

Subsequence: [1,2,4] - is not continous but maintains relative order of elements

Subset: [1,3,2] - is not continous and does not maintain relative order of elements

# Heap

A common misconception is that a Heap is the same as a Priority Queue, which is not true. A priority queue is an abstract data type, while a Heap is a data structure. Therefore, a Heap is not a Priority Queue, but a way to implement a Priority Queue.

How to determine a node is leave? : total nodes number n divided by 2, if index > n/2 then this is a leave.



