## Part 2: Two Pointer Problem

-[**283(Easy). Move Zeroes**](https://leetcode.com/problems/move-zeroes/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given an integer array nums, move all 0's to the end of it while maintaining the relative order of the non-zero elements.
  - Note that you must do this in-place without making a copy of the array.

  **Solution (Python): **
  ```python
  class Solution(object):
    def moveZeroes(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """
        
        insert_pos = 0
        
        for num in nums:
            if num != 0:
                nums[insert_pos] = num
                insert_pos += 1
        
        while insert_pos < len(nums):
            nums[insert_pos] = 0
            insert_pos += 1

        return nums
```

-[**392(Easy). Is Subsequence**](https://leetcode.com/problems/is-subsequence/?envType=study-plan-v2&envId=leetcode-75)
  - Given two strings s and t, return true if s is a subsequence of t, or false otherwise.
  - A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).
  - Considering the case s is empty.

  **Solution (Python): **
  ```python
  class Solution(object):
    def isSubsequence(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """

        i = 0
        j = 0
        while i < len(s) and j < len(t):
            if s[i] == t[j]:
                i+=1
            j+=1
        return True if i == len(s) else False
```

-[**11(Medium). Container With Most Water**](https://leetcode.com/problems/is-subsequence/?envType=study-plan-v2&envId=leetcode-75)
  - You are given an integer array height of length n. There are n vertical lines drawn such that the two endpoints of the ith line are (i, 0) and (i, height[i]).
  - Find two lines that together with the x-axis form a container, such that the container contains the most water.
  - Return the maximum amount of water a container can store.
  - Notice that you may not slant the container.

  **Solution (Python): **
  ```python
class Solution(object):
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        
        n = len(height)
        left, right = 0, n - 1
        max_area = 0
    
        while left < right:
            # Calculate current area
            current_area = min(height[left], height[right]) * (right - left)
            # Update max_area if current area is greater
            max_area = max(max_area, current_area)
        
            # Move the pointer with the shorter line towards the center
            if height[left] < height[right]:
                left += 1
            else:
                right -= 1
    
        return max_area
 ```
-[**1679(Medium). Max Number of K-Sum Pairs**](https://leetcode.com/problems/max-number-of-k-sum-pairs/description/?envType=study-plan-v2&envId=leetcode-75)
  - You are given an integer array nums and an integer k.
  - In one operation, you can pick two numbers from the array whose sum equals k and remove them from the array.
  - Return the maximum number of operations you can perform on the array.

  **Solution (Python): **
  ```python
class Solution(object):
    def maxOperations(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        freq = {}
        operations = 0
        
        for num in nums:
            complement = k - num
            if complement in freq and freq[complement] > 0:
                operations += 1
                freq[complement] -= 1
            elif num not in freq:
                freq[num] = 1
            else:
                # If complement is not found and num is already in freq,
                # increment the frequency count for num
                freq[num] += 1
        
        return operations

 ``` 

-[**125(Easy). Valid Palindrome**](https://leetcode.com/problems/valid-palindrome/description/)
  - A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.
  - Given a string s, return true if it is a palindrome, or false otherwise.

  **Solution (Python): **
  ```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        cleaned = ''.join(c.lower() for c in s if c.isalnum())
        left, right = 0, len(cleaned)-1

        while left < right:
            if cleaned[left] != cleaned[right]:
                return False
            left+=1
            right-=1
        return True
 ```
  **Solution (Python): **
  ```python
class Solution(object):
    def isPalindrome(self, s):
        """
        :type s: str
        :rtype: bool
        """
        # p = re.sub('[^a-z0-9]', '', s.lower())
        p = "".join(re.findall("[A-Za-z0-9]+", s)).lower()
        return p == p[::-1]
 ``` 


-[**15(Medium). 3Sum**](https://leetcode.com/problems/3sum/description/)
  - Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.
  - Notice that the solution set must not contain duplicate triplets.

  **Solution (Python): **
  ```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        output = set()
        for i in range(len(nums)):
            j = i + 1
            k = len(nums) - 1
            while j < k:
                total = nums[i] + nums[j] + nums[k]
                if total == 0:
                    output.add((nums[i], nums[j], nums[k]))
                    j += 1
                    k -= 1
                elif total < 0:
                    j += 1
                else:
                    k -= 1
        return list(output)
 ```
  **Solution (Python): **
  ```python
class Solution(object):
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        # Initialize lists to hold negative, positive, and zero numbers
        negative_nums = []
        positive_nums = []
        zero_nums = []
        
        # Initialize a set to store the result
        result = set()
        
        # Iterate through the input list and categorize numbers
        for num in nums:
            if num < 0:
                negative_nums.append(num)
            elif num > 0:
                positive_nums.append(num)
            else:
                zero_nums.append(num)
        
        # Convert lists to sets for faster lookup
        negative_set = set(negative_nums)
        positive_set = set(positive_nums)
        
        # Case when zero exists in the input list
        if zero_nums:
            for num in positive_set:
                reciprocal = -1 * num
                if reciprocal in negative_set:
                    result.add(tuple([num, 0, -num]))
        
        # Case when there are at least three zeros
        if len(zero_nums) >= 3:
            result.add((0, 0, 0))
        
        # Check combinations of two negative numbers and one positive number
        for i in range(len(negative_nums)):
            for j in range(i + 1, len(negative_nums)):
                target = -1 * (negative_nums[i] + negative_nums[j])
                if target in positive_set:
                    result.add(tuple(sorted([negative_nums[i], negative_nums[j], target])))
        
        # Check combinations of two positive numbers and one negative number
        for i in range(len(positive_nums)):
            for j in range(i + 1, len(positive_nums)):
                target = -1 * (positive_nums[i] + positive_nums[j])
                if target in negative_set:
                    result.add(tuple(sorted([positive_nums[i], positive_nums[j], target])))
        
        return result
 ```
