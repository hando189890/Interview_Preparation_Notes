## Part : Binary Search Problems: 

- [**LeetCode (Medium).153. Find Minimum in Rotated Sorted Array**](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)
  - Suppose an array of length n sorted in ascending order is rotated between 1 and n times. For example, the array nums = [0,1,2,4,5,6,7] might become:
    - [4,5,6,7,0,1,2] if it was rotated 4 times.
    - [0,1,2,4,5,6,7] if it was rotated 7 times.
  - Notice that rotating an array [a[0], a[1], a[2], ..., a[n-1]] 1 time results in the array [a[n-1], a[0], a[1], a[2], ..., a[n-2]].
  - Given the sorted rotated array nums of unique elements, return the minimum element of this array.
  - You must write an algorithm that runs in O(log n) time.
   
  **Solution (Python): **
  ```python
  class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        left, right = 0, len(nums) - 1
        
        # The binary search
        while left < right:
            mid = left + (right - left) // 2
            
            # If middle element is greater than the rightmost element,
            # the smallest element is in the right half
            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                # If middle element is less than or equal to the rightmost element,
                # the smallest element is in the left half (including mid)
                right = mid
  ```

- [**LeetCode (Medium).33. Search in Rotated Sorted Array**](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)
  - There is an integer array nums sorted in ascending order (with distinct values).
  - Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
  - Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
  - You must write an algorithm with O(log n) runtime complexity.
   
  **Solution (Python): **
  ```python
  class Solution(object):
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left, right = 0, len(nums) - 1

        while left <= right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return mid

            # If left half is sorted
            if nums[left] <= nums[mid]:
                # Check if target is in the left half
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            # If right half is sorted
            else:
                # Check if target is in the right half
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1

        return -1
  ```
