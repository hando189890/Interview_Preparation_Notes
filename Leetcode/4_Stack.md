## Part 4: Stack

-[**LeetCode Easy). 20. Valid Parentheses**](https://leetcode.com/problems/valid-parentheses/description/)
  - Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
  - An input string is valid if:
    - Open brackets must be closed by the same type of brackets.
    - Open brackets must be closed in the correct order.
    - Every close bracket has a corresponding open bracket of the same type.
   
  **Solution (Python): **
  ```python
  class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = [] # create an empty stack to store opening brackets
        for c in s: # loop through each character in the string
            if c in '([{': # if the character is an opening bracket
                stack.append(c) # push it onto the stack
            else: # if the character is a closing bracket
                if not stack or \
                    (c == ')' and stack[-1] != '(') or \
                    (c == '}' and stack[-1] != '{') or \
                    (c == ']' and stack[-1] != '['):
                    return False # the string is not valid, so return false
                stack.pop() # otherwise, pop the opening bracket from the stack
        return not stack # if the stack is empty, all opening brackets have been matched with their corresponding closing brackets,
                         # so the string is valid, otherwise, there are unmatched opening brackets, so return false
```
  ```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        mapping = {"(":")", "{":"}", "[":']'}
        stack = []

        for c in s:
            if c in ["(", "{", "["]:
                stack.append(mapping[c])
            else:
                if len(stack)==0 or stack.pop() != c:
                    return False
        
        return True if not stack else False
```
