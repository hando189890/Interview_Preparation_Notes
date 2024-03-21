## Part 3: Sliding Windows

-[**LeetCode 121(Easy). Best Time to Buy and Sell Stock**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
  - You are given an array prices where prices[i] is the price of a given stock on the ith day.
  - You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
  - Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

  **Solution (Python): **
  ```python
  class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) < 2:
            return 0  # If there are less than 2 prices, no profit can be made
        
        min_price = prices[0]  # Initialize the minimum price to the first price
        max_profit = 0  # Initialize the maximum profit to 0
        
        for price in prices[1:]:  # Start iterating from the second price
            if price < min_price:
                min_price = price  # Update the minimum price if a lower price is found
            else:
                max_profit = max(max_profit, price - min_price)  # Update max profit if selling at current price is profitable
        
        return max_profit
```
**Solution (Python): **
  ```python
  class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        min_val_found = prices[0]
        max_rent = 0
        
        for p in prices:
            if p < min_val_found:
                min_val_found = p
            if p - min_val_found > max_rent:
                max_rent = p - min_val_found
                
        return max_rent
```

-[**LeetCode 3(Medium). Longest Substring Without Repeating Characters**](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)
  - Given a string s, find the length of the longest substring without repeating characters.
  **Solution (Python): **
  ```python
  class Solution(object):
    def lengthOfLongestSubstring(self, s):
        """
        :type s: str
        :rtype: int
        """
        if not s:
            return 0
        
        covered = set()
        max_length = 0
        left = 0
        
        for right in range(len(s)):
            while s[right] in covered:
                covered.remove(s[left])
                left += 1
            covered.add(s[right])
            max_length = max(max_length, right - left + 1)
        
        return max_length
```

-[**LeetCode (Medium). 424. Longest Repeating Character Replacement**](https://leetcode.com/problems/longest-repeating-character-replacement/description/)
  - You are given a string s and an integer k. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most k times.
  - Return the length of the longest substring containing the same letter you can get after performing the above operations.
  **Solution (Python): **
  ```python
  class Solution(object):
    def characterReplacement(self, s, k):
        """
        :type s: str
        :type k: int
        :rtype: int
        """
        max_length = 0
        max_count = 0
        char_count = {}
        left = 0

        for right in range(len(s)):
            char_count[s[right]] = char_count.get(s[right], 0) + 1
            max_count = max(max_count, char_count[s[right]])
            
            # If the window size - max_count > k, move the left pointer
            if right - left + 1  > max_count + k:
                char_count[s[left]] -= 1
                left += 1
            
            max_length = max(max_length, right - left + 1)

        return max_length
```
-[**LeetCode (Hard). 76. Minimum Window Substring**](https://leetcode.com/problems/minimum-window-substring/description/)
  - Given two strings s and t of lengths m and n respectively, return the minimum window 
substring of s such that every character in t (including duplicates) is included in the window. If there is no such substring, return the empty string "".
  - The testcases will be generated such that the answer is unique.
**Solution (Python): **
  ```python
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        if not s or not t:
            return ""

        # Dictionary to count all characters in t
        char_freq_t = {}
        for char in t:
            char_freq_t[char] = char_freq_t.get(char, 0) + 1

        # Number of unique characters in t that need to be present in the window
        required_unique_chars = len(char_freq_t)
        
        # Initialize left and right pointers, and the number of characters that meet the frequency requirement
        left, right = 0, 0
        formed = 0

        # Window counts for characters in the current window
        window_counts = {}

        # Answer format: (window length, left index, right index). Initialize with -1 as window length to indicate no window found yet
        answer = [-1, 0, 0]

        while right < len(s):
            # Add the current character to the window
            current_char = s[right]
            window_counts[current_char] = window_counts.get(current_char, 0) + 1

            # Check if the current character's frequency matches the required frequency in t
            if current_char in char_freq_t and window_counts[current_char] == char_freq_t[current_char]:
                formed += 1

            # Try to shrink the window from the left if all required characters are present
            while left <= right and formed == required_unique_chars:
                current_char = s[left]

                # Update answer if the current window is smaller than the previously found smallest window
                if answer[0] == -1 or (right - left + 1) < answer[0]:
                    answer = [right - left + 1, left, right]

                # Remove the leftmost character from the window
                window_counts[current_char] -= 1
                if current_char in char_freq_t and window_counts[current_char] < char_freq_t[current_char]:
                    formed -= 1

                left += 1

            right += 1

        # Return the minimum window substring or an empty string if no such window exists
        return "" if answer[0] == -1 else s[answer[1]: answer[2] + 1]
```
