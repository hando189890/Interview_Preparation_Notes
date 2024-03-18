## Part 1: Arrary and String Problem

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

- [**238(Medium. Product of Array Except Self**](https://leetcode.com/problems/product-of-array-except-self/description/?envType=study-plan-v2&envId=leetcode-75)
  - Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].
  - The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
  - You must write an algorithm that runs in O(n) time and without using the division operation.

   **Solution (Python): **
  _Time Complexity: O(N) + Space Comexity: O(N)_
  ```python
  class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
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
