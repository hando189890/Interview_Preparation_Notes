## Part 1: Arrary String and Hashing Problem

- [**Leetcode 1768 (Easy): Merge Strings Alternately**](https://leetcode.com/problems/merge-strings-alternately/description/?envType=study-plan-v2&envId=leetcode-75)
  - You are given two strings word1 and word2. Merge the strings by adding letters in alternating order, starting with word1. If a string is longer than the other, append the additional letters onto the end of the merged string.
  - Return the merged string.

  **Solution (Python): **
  ```python
  class Solution(object):
    def mergeAlternately(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: str
        """
        final_string = ""

        m = len(word1)
        n = len(word2)

        k = min(m, n)
        for i in range(k):
            final_string += word1[i] + word2[i]

        if m < n:
            final_string += word2[k:]
        elif m > n:
            final_string += word1[k:]

        return final_string


- [**1071(Easy):Greatest Common Divisor of Strings**](https://leetcode.com/problems/greatest-common-divisor-of-strings/description/?envType=study-plan-v2&envId=leetcode-75)
  - For two strings s and t, we say "t divides s" if and only if s = t + t + t + ... + t + t (i.e., t is concatenated with itself one or more times).\n
  - Given two strings str1 and str2, return the largest string x such that x divides both str1 and str2.

   **Solution 1 (Python): **
  ```python
  class Solution(object):
    def gcd(self, a, b):
        while b:
            a, b = b, a % b
        return a
        
    def gcdOfStrings(self, str1, str2):
        if str1 + str2 != str2 + str1:
            return ""
        
        gcd_length = self.gcd(len(str1), len(str2))
        
        return str1[:gcd_length]
  ```
     **Solution 2 (Python): **
    ```python
    class Solution(object):
        def gcdOfStrings(self, str1, str2):
          if str1 + str2 != str2 + str1:
            return ""
          if len(str1) == len(str2):
            return str1
          if len(str1) > len(str2):
            return self.gcdOfStrings(str1[len(str2):], str2)
          return self.gcdOfStrings(str1, str2[len(str1):])

    
- [**1431(Easy). Kids With the Greatest Number of Candies**](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/description/?envType=study-plan-v2&envId=leetcode-75)
  - There are n kids with candies. You are given an integer array candies, where each candies[i] represents the number of candies the ith kid has, and an integer extraCandies, denoting the number of extra candies that you have.
  - Return a boolean array result of length n, where result[i] is true if, after giving the ith kid all the extraCandies, they will have the greatest number of candies among all the kids, or false otherwise.
  - Note that multiple kids can have the greatest number of candies.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def kidsWithCandies(self, candies, extraCandies):
        """
        :type candies: List[int]
        :type extraCandies: int
        :rtype: List[bool]
        """

        maxCandies = max(candies)
        result = []
        
        for c in candies:
            if c + extraCandies >= maxCandies:
                result.append(True)
            else:
                result.append(False)
        return result
  
  ```

- [**605(Easy). Can Place Flowers**](https://leetcode.com/problems/can-place-flowers/description/?envType=study-plan-v2&envId=leetcode-75)
  - You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in adjacent plots.
  - Given an integer array flowerbed containing 0's and 1's, where 0 means empty and 1 means not empty, and an integer n, return true if n new flowers can be planted in the flowerbed without violating the no-adjacent-flowers rule and false otherwise.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(1)_
  ```python
  class Solution(object):
    def canPlaceFlowers(self, flowerbed, n):
        """
        :type flowerbed: List[int]
        :type n: int
        :rtype: bool
        """
        for i in range(len(flowerbed)):
            if flowerbed[i] == 0:
                if (i == 0 or flowerbed[i - 1] == 0) and (i == len(flowerbed) - 1 or flowerbed[i + 1] == 0):
                    n -= 1
                    flowerbed[i] = 1
        
        return n <= 0 
        # if n becomes less than or equal to zero after placing flowers, the function returns True. 
  ```

- [**345(Easy). Reverse Vowels of a String**](https://leetcode.com/problems/reverse-vowels-of-a-string/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given a string s, reverse only all the vowels in the string and return it.
  - The vowels are 'a', 'e', 'i', 'o', and 'u', and they can appear in both lower and upper cases, more than once.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def reverseVowels(self, s):
        """
        :type s: str
        :rtype: str
        """
        vowels = {'a', 'e', 'i', 'o', 'u'}
        s = list(s)
        left, right = 0, len(s) - 1
        
        while left < right:
            if s[left].lower() in vowels and s[right].lower() in vowels:
                s[left], s[right] = s[right], s[left]
                left += 1
                right -= 1
            elif s[left].lower() in vowels:
                right -= 1
            elif s[right].lower() in vowels:
                left += 1
            else:
                left += 1
                right -= 1
        
        return ''.join(s)
  ```
- [**151(Medium). Reverse Words in a String**](https://leetcode.com/problems/reverse-words-in-a-string/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given an input string s, reverse the order of the words.
  - A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.
  - Return a string of the words in reverse order concatenated by a single space.
  - Note that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        s = s.split()
        # It splits the string s into a list of substrings using whitespace (spaces, tabs, or newlines) as the default delimiter.

        # Two pointers approach
        left, right = 0, len(s) - 1

        while left < right:
            # Swap the words
            s[left], s[right] = s[right], s[left]
            # Move pointers
            left += 1
            right -= 1

        # Convert the list back to a string
        return ' '.join(s)
        # ' '.join(s) concatenates all the words in the list s into a single string with spaces between them.
        
  ```

- [**238(Medium). Product of Array Except Self**](https://leetcode.com/problems/product-of-array-except-self/description/?envType=study-plan-v2&envId=leetcode-75)
  - **IMPORTANT !!!**
  - Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].
  - The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
  - You must write an algorithm that runs in O(n) time and without using the division operation.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution:
    def productExceptSelf(self, nums):
        n = len(nums)
        ans = [1] * n
        l = 1
        r = n - 2
        prefix = 1
        suffix = 1
        while l <= n and r >= 0:
            prefix *= nums[l-1]
            suffix *= nums[r+1]
            ans[l] *= prefix
            ans[r] *= suffix
            l += 1
            r -= 1
        return ans
  ```

- [**334(Medium). Increasing Triplet Subsequence**](https://leetcode.com/problems/increasing-triplet-subsequence/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given an integer array nums, return true if there exists a triple of indices (i, j, k) such that i < j < k and nums[i] < nums[j] < nums[k]. If no such indices exists, return false.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(1)_
  ```python
  class Solution(object):
    def increasingTriplet(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        first = second = float('inf')
        for num in nums:
            if num <= first:
                first = num
            elif num <= second:
                second = num
            else:
                return True
        return False

- [**443(Medium). String Compression**](https://leetcode.com/problems/string-compression/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given an array of characters chars, compress it using the following algorithm:
  - Begin with an empty string s. For each group of consecutive repeating characters in chars:
    - If the group's length is 1, append the character to s.
    - Otherwise, append the character followed by the group's length.
  - The compressed string s should not be returned separately, but instead, be stored in the input character array chars. Note that group lengths that are 10 or longer will be split into multiple characters in chars.
  - After you are done modifying the input array, return the new length of the array.
  - You must write an algorithm that uses only constant extra space

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(1)_
  ```python
  class Solution(object):
    def compress(self, chars):
        """
        :type chars: List[str]
        :rtype: int
        """
        ans = 0
        i = 0

        while i < len(chars):
            letter = chars[i]
            count = 0
            
            # Count consecutive repeating characters
            while i < len(chars) and chars[i] == letter:
                count += 1
                i += 1
    
            # Write the character
            chars[ans] = letter
            ans += 1
            
            # If count > 1, write the count (as string) next to the character
            if count > 1:
                for c in str(count):
                    chars[ans] = c
                    ans += 1

        return ans

- [**217(Easy). Contains Duplicate**](https://leetcode.com/problems/contains-duplicate/description/)
  - Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def containsDuplicate(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        return len(nums) != len(set(nums))
  ```

- [**242(Easy). Valid Anagram**](https://leetcode.com/problems/valid-anagram/description/)
  - Given two strings s and t, return true if t is an anagram of s, and false otherwise.
  - An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def isAnagram(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: bool
        """
        # In case of different length of thpse two strings...
        if len(s) != len(t):
            return False
        for idx in set(s):
        # Compare s.count(l) and t.count(l) for every index i from 0 to 26...
            # If they are different, return false...
            if s.count(idx) != t.count(idx):
                return False
        return True     # Otherwise, return true...
  ```

- [**1. Two Sum**](https://leetcode.com/problems/two-sum/description/)
  - Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
  - You may assume that each input would have exactly one solution, and you may not use the same element twice.
  - You can return the answer in any order.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        hashset = {}  # Create an empty dictionary to store indices
        for i, num in enumerate(nums):  # Fix syntax error here
            diff = target - num
            if diff in hashset and hashset[diff] != i:  # Check if the complement exists and it's not the same index
                return [hashset[diff], i]  # Return the indices
            hashset[num] = i  # Store the index of the current number
        return None  # Return None if no solution is found
  ```
- [**49(Medium). Group Anagrams**](https://leetcode.com/problems/group-anagrams/description/)
  - Given an array of strings strs, group the anagrams together. You can return the answer in any order.
  - An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

   **Solution One (Python): **
  _Time Complexity: O(n*m) _
  ```python
  class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        dic = collections.defaultdict(list)
        for i in strs:
            c = [0] * 26
            for ch in i:
                c[ord(ch)-ord('a')] += 1
            dic[tuple(c)].append(i)
        return dic.values()
  ```
     **Solution Two (Python): **
  _Time Complexity: O(n*klogn) _
  ```python
  class Solution(object):
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        group_dict = {}
        for word in strs:
            cur = tuple(sorted(word))  # Convert list to tuple
            # Stored as group_dict = {(u'a', u'b', u't'): [u'bat'], (u'a', u'e', u't'): [u'eat', u'tea', u'ate'], (u'a', u'n', u't'): [u'tan', u'nat']}
            '''
            cur = ''.join(sorted(word))
            Stored as group_dict = {u'ant': [u'tan', u'nat'], u'abt': [u'bat'], u'aet': [u'eat', u'tea', u'ate']}
            '''
            if cur in group_dict:
                group_dict[cur].append(word)
            else:
                group_dict[cur] = [word]
        print(group_dict)
        return list(group_dict.values())
  ```

- [**347(Medium). Top K Frequent Elements**](https://leetcode.com/problems/top-k-frequent-elements/description/)
  - Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

   **Solution One (Python): **
  ```python
  class Solution(object):
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        counts = {}
        for num in nums:
            counts[num] = counts.get(num, 0) + 1
            
        # Sort the dictionary by values (frequencies) in descending order
        sorted_counts = sorted(counts.items(), key=lambda x: x[1], reverse=True)
    
        # Get the first k elements from the sorted dictionary
        top_k = [item[0] for item in sorted_counts[:k]]
    
        return top_k
  ```

- [**128(Medium). Longest Consecutive Sequence**](https://leetcode.com/problems/longest-consecutive-sequence/description/)
  - Given an unsorted array of integers nums, return the length of the longest consecutive elements sequence.
  - You must write an algorithm that runs in O(n) time.

   **Solution One (Python): **
  ```python
  class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        num_set = set(nums)
        max_length = 0
        for num in num_set:
            # Check if num is the start of a new consecutive sequence
            if num - 1 not in num_set:
                current_num = num
                current_length = 1

                # Count the length of the consecutive sequence
                while current_num + 1 in num_set:
                    current_num += 1
                    current_length += 1

            max_length = max(max_length, current_length)

        return max_length
  ```

- [**532(Medium). K-diff Pairs in an Array**](https://leetcode.com/problems/k-diff-pairs-in-an-array/description/)
  - Given an array of integers nums and an integer k, return the number of unique k-diff pairs in the array.
  - A k-diff pair is an integer pair (nums[i], nums[j]), where the following are true:
    - 0 <= i, j < nums.length
    - i != j
    - |nums[i] - nums[j]| == k
  - Notice that |val| denotes the absolute value of val.

   **Solution One (Python): **
  ```python
  class Solution(object):
    def findPairs(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """ 
       
        hashset = set(nums)
        counter = Counter(nums)
        finalset = set()

        for n in nums:
            if k == 0:
                return sum(1 for num, count in counter.items() if count > 1)
            
            if n - k in hashset:
                finalset.add(tuple(sorted([n, n - k])))
            if n + k in hashset:
                finalset.add(tuple(sorted([n, n + k])))

        return len(finalset)
  ```
     **Solution Two (Python): **
  ```python
class Solution(object):
    def findPairs(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """ 
        if k != 0:
            count = 0
            nums = set(nums)
            for i in nums:
                if i + k in nums:
                    count += 1
            return count
        else:
            count = 0
            nums_set = set(nums)
            for i in nums_set:
                if nums.count(i) > 1:
                    count += 1
            return count
  ```
