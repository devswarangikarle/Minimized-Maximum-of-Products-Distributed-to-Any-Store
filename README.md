# Minimized-Maximum-of-Products-Distributed-to-Any-Store

You are given an integer n indicating there are n specialty retail stores. There are m product types of varying amounts, which are given as a 0-indexed integer array quantities, where quantities[i] represents the number of products of the ith product type.

You need to distribute all products to the retail stores following these rules:

A store can only be given at most one product type but can be given any amount of it.
After distribution, each store will have been given some number of products (possibly 0). Let x represent the maximum number of products given to any store. You want x to be as small as possible, i.e., you want to minimize the maximum number of products that are given to any store.
Return the minimum possible x.

class Solution:
    def minimizedMaximum(self, n: int, quantities: List[int]) -> int:
        def canDistribute(max_products: int) -> bool:
            # Calculate the number of stores needed for each product type
            stores_needed = sum((quantity + max_products - 1) // max_products for quantity in quantities)
            # Check if we can manage with `n` stores
            return stores_needed <= n

        # Binary search range
        left, right = 1, max(quantities)
        
        # Perform binary search
        while left < right:
            mid = (left + right) // 2
            if canDistribute(mid):
                right = mid  # Try for a smaller max
            else:
                left = mid + 1  # Increase max products per store
        
        return left
