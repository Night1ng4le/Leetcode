

# The LeetCode Beginner's Guide（Attemped）

[toc]

## Solving Your First Problem 

### [2235. Add two Numbers](https://leetcode.com/problems/add-two-integers/)

#### Solution

```c++
class Solution {
public:
    int sum(int num1, int num2) {
        return num1 + num2;
    }
};
```

### [226. Invert Binary Tree](https://leetcode.com/problems/invert-binary-tree/)

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

```
Input: root = [2,1,3]
Output: [2,3,1]
```

**Example 3:**

```
Input: root = []
Output: []
```

#### Solution

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if(root == NULL) {
            return NULL;
        }
        invertTree(root->left);
        invertTree(root->right);
        TreeNode* x = root->left;
        root->left = root->right;
        root->right = x;
        return root;
    }
}; 
// Recurision
```

## Challenge Problems

### [1480. Running Sum of 1d Array](https://leetcode.com/problems/running-sum-of-1d-array/)

Given an array `nums`. We define a running sum of an array as `runningSum[i] = sum(nums[0]…nums[i])`.

Return the running sum of `nums`.

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [1,3,6,10]
Explanation: Running sum is obtained as follows: [1, 1+2, 1+2+3, 1+2+3+4].
```

**Example 2:**

```
Input: nums = [1,1,1,1,1]
Output: [1,2,3,4,5]
Explanation: Running sum is obtained as follows: [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1].
```

**Example 3:**

```
Input: nums = [3,1,2,10,1]
Output: [3,4,6,16,17]
```

#### Solution 1

Double circle - from tail to head	

```c++
//O(n^2)
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        for(int i = nums.size() - 1; i >= 0; i--) {
            for(int j = 0; j < i; j++) {
                nums[i] += nums[j];
            }
        }
        return nums;
    }
};
```

#### Solution 2

An easy way: Start from the 2nd element, and each result only need sum the previous value.

```c++
//O(n) 
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        for(int i = 1; i < nums.size(); i++) {
            nums[i] += nums[i-1];
        }
        return nums;
        //time complexity = O(n)
        //space complexity = O(1)
    }
};
```

### [1672. Richest Customer Wealth](https://leetcode.com/problems/richest-customer-wealth/) - Attempted

You are given an `m x n` integer grid `accounts` where `accounts[i][j]` is the amount of money the `ith` customer has in the `jth` bank. Return *the **wealth** that the richest customer has.*

A customer's **wealth** is the amount of money they have in all their bank accounts. The richest customer is the customer that has the maximum **wealth**.

**Example 1:**

```
Input: accounts = [[1,2,3],[3,2,1]]
Output: 6
Explanation:
1st customer has wealth = 1 + 2 + 3 = 6
2nd customer has wealth = 3 + 2 + 1 = 6
Both customers are considered the richest with a wealth of 6 each, so return 6.
```

**Example 2:**

```
Input: accounts = [[1,5],[7,3],[3,5]]
Output: 10
Explanation: 
1st customer has wealth = 6
2nd customer has wealth = 10 
3rd customer has wealth = 8
The 2nd customer is the richest with a wealth of 10.
```

**Example 3:**

```
Input: accounts = [[2,8,7],[7,1,3],[1,9,5]]
Output: 17
```

#### Solution

```c++

```

###  [412. Fizz Buzz](https://leetcode.com/problems/fizz-buzz/)

Given an integer `n`, return *a string array* `answer` *(**1-indexed**) where*:

- `answer[i] == "FizzBuzz"` if `i` is divisible by `3` and `5`.
- `answer[i] == "Fizz"` if `i` is divisible by `3`.
- `answer[i] == "Buzz"` if `i` is divisible by `5`.
- `answer[i] == i` (as a string) if none of the above conditions are true.

**Example 1:**

```
Input: n = 3
Output: ["1","2","Fizz"]
```

**Example 2:**

```
Input: n = 5
Output: ["1","2","Fizz","4","Buzz"]
```

**Example 3:**

```
Input: n = 15
Output: ["1","2","Fizz","4","Buzz","Fizz","7","8","Fizz","Buzz","11","Fizz","13","14","FizzBuzz"]
```

#### Solution

```c++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> ans(n);
        for (int i = 1; i <= n; i++) {
            if (i % 3 == 0 && i % 5 == 0) {
                ans[i-1] = "FizzBuzz";
            } else if (i % 3 == 0) {
                ans[i-1] = "Fizz";
            } else if (i % 5 == 0) {
                ans[i-1] = "Buzz";
            } else {
                ans[i-1] = to_string(i);
            }
        }
        return ans;
    }
};
```

### [1342. Number of Steps to Reduce a Number to Zero](https://leetcode.com/problems/number-of-steps-to-reduce-a-number-to-zero/)

Given an integer `num`, return *the number of steps to reduce it to zero*.

In one step, if the current number is even, you have to divide it by `2`, otherwise, you have to subtract `1` from it.

**Example 1:**

```
Input: num = 14
Output: 6
Explanation: 
Step 1) 14 is even; divide by 2 and obtain 7. 
Step 2) 7 is odd; subtract 1 and obtain 6.
Step 3) 6 is even; divide by 2 and obtain 3. 
Step 4) 3 is odd; subtract 1 and obtain 2. 
Step 5) 2 is even; divide by 2 and obtain 1. 
Step 6) 1 is odd; subtract 1 and obtain 0.
```

**Example 2:**

```
Input: num = 8
Output: 4
Explanation: 
Step 1) 8 is even; divide by 2 and obtain 4. 
Step 2) 4 is even; divide by 2 and obtain 2. 
Step 3) 2 is even; divide by 2 and obtain 1. 
Step 4) 1 is odd; subtract 1 and obtain 0.
```

**Example 3:**

```
Input: num = 123
Output: 12
```

#### Solution  

```c++
class Solution {
public:
    int numberOfSteps(int num) {
        int cnt = 0;
        while(0 < num) {
            if(num % 2 == 0) {
                num = num / 2;
            }else{
                num = num - 1;
            }
            cnt = cnt + 1;
        }
        return cnt;
    }
};
```

### [876. Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/)

Given the `head` of a singly linked list, return *the middle node of the linked list*.

If there are two middle nodes, return **the second middle** node.

**Example 1:**

![img](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg)

```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```

**Example 2:**

![img](https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg)

```
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

#### Solution 1 - Simulation

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* temp = head;
        int cnt = 1;
        while (temp->next != NULL) {
            temp = temp->next;
            cnt = cnt + 1;
        }
        temp = head;
        cnt = cnt / 2;
        while (cnt > 0) {
            temp = temp->next;
            cnt = cnt - 1;
        }
        return temp;
    }
};
```

#### Solution 2 - Based on math

```c++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        
    ListNode* s=head;
    ListNode* f=head;
       
       while(f!=NULL&&f->next!=NULL){

           f=f->next->next;
           s=s->next;
       }
        return s;

    }
};
```

### [383. Ransom Note](https://leetcode.com/problems/ransom-note/)

Given two strings `ransomNote` and `magazine`, return `true` *if* `ransomNote` *can be constructed by using the letters from* `magazine` *and* `false` *otherwise*.

Each letter in `magazine` can only be used once in `ransomNote`.

**Example 1:**

```
Input: ransomNote = "a", magazine = "b"
Output: false
```

**Example 2:**

```
Input: ransomNote = "aa", magazine = "ab"
Output: false
```

**Example 3:**

```
Input: ransomNote = "aa", magazine = "aab"
Output: true
```

#### Solution

```c++
```

