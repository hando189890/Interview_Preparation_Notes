## Part 3: Sliding Windows

-[**121(Easy). Best Time to Buy and Sell Stock**](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)
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



