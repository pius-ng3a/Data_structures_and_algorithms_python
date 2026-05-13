# Data_structures_and_algorithms_python
This repository contains some tasks and their solutions to demonstrate effective use of data structures and algorithms in Python.

**Problem 1**:

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

 

Example 1:

Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:

Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:

Input: nums = [3,3], target = 6
Output: [0,1]

 

Constraints:

    2 <= nums.length <= 104
    -109 <= nums[i] <= 109
    -109 <= target <= 109
    Only one valid answer exists.
    
**Solution 1**:
```
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        # We'll use a hashmap (dictionary) to store every seen element and its index. We would compare 
        # new elements with all seen elements. If any two visited elements sum up to the target, we report
        # the indices of the two elements whose sum equals target. 
        # This implementation runs in O(n) since in the worst case scenario, all elements in the array
        # visited once.
        numbers_index ={}
        for index,num in enumerate(nums):
            if (target-num) in numbers_index:
                return(index, numbers_index[target - num])
            numbers_index[num] = index
        return ()
```



**Problem 2**:

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

  1. Open brackets must be closed by the same type of brackets.
  2. Open brackets must be closed in the correct order.
  3. Every close bracket has a corresponding open bracket of the same type.

 

Example 1:

Input: s = "()"

Output: true

Example 2:

Input: s = "()[]{}"

Output: true

Example 3:

Input: s = "(]"

Output: false

Example 4:

Input: s = "([])"

Output: true

Example 5:

Input: s = "([)]"

Output: false

 

Constraints:

    1 <= s.length <= 104
    s consists of parentheses only '()[]{}'.

**Solution 2**:

We use a stack to store seen openning brackets and a dictionary to hold the corresponding openning and closing brakets. We then traverse the given string from left to rights. When an oppening 
bracket is encountered, we add it to the top of the stack. When a closing bracket is encountered, we check if the stack is empty or if the openning bracket at the top of the stack is not the matching one. If either of these conditions is reached, we conclude that the string is not well formated. If the character at the top of the stack is the correct opening bracket, we remove it and keep traversing the string.

This algorithm has a time complexity of O(n), where n is the string length. We add and remove an element from a stack at O(1) time complexity. 
```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        #store the characters of the string in a dictionary
        characters = {")":"(","}":"{","]":"["}
        # stack to hold each opening bracket
        stack = []
        for character in s:
            if character in characters:
                #if a closing bracket is encountered, check if the stack already contains at least 1
                # opening bracket, and if the top opening bracket in the stack corresponds to current
                #bracket
                if not stack or stack[-1] != characters[character]:
                    return False
                else:
                    stack.pop()
            else:
                stack.append(character)
        return True
```
