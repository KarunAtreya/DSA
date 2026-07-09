
## Arrays and String DSA problems:

## 1. Find the closest number to zero

### Problem: 

Given an array of integers, return the number closest to zero. If there are two equally close
values (one negative and one positive), return the positive one. For example, given the input
  [-4, -2, 1, 4, 2], both -2 and 2 are at the same distance from zero, but the correct answer s 2.

### Understanding the Problem: Find Closest Number to Zero

The Find Closest Number to Zero problem is a classic array algorithm challenge frequently encountered in technical interviews and coding practice platforms like LeetCode. The objective is to identify the integer in a list that is numerically closest to zero. If there is a tie — for instance, both -2 and 2 — the positive number should be returned.

### Algorithmic Approach
This problem is typically solved using a linear scan algorithm. We initialize a variable, commonly called closest, with the first value of the array. As we iterate through the array, we compare each element using absolute value comparison:

If the absolute value of the current number is less than that of closest, update closest.
If the absolute values are the same, choose the positive number.
This logic ensures that we return the number closest to zero and correctly handle tie-breakers in favor of positive values.

### Time and Space Complexity
time = O(n)
space = O(1)

### Edge Cases
This problem requires careful attention to detail. Common edge cases include:
An array containing only one element
Presence of both x and -x
All elements being negative or all being positive
Correct handling of these edge cases ensures robustness and correctness of the algorithm.

### Use Cases and Relevance
Sensor data normalization,Financial deviation analysis, Error minimization logic\


## 2. Merge Strings Alternatively

### Problem
You are given two strings, word1 and word2. The task is to create a new string by merging characters alternately from each input. You begin with the first character of word1, followed by the first character of word2, then the second from word1, and so on. This continues until all characters from both strings are used. If one string is longer than the other, the remaining characters from the longer string are appended at the end.

### Solution

    def mergeAlternately(self, word1: str, word2: str) -> str:
            A, B = len(word1), len(word2)
            counter = 0
            string_list = []
            
            while counter < A and counter < B:
                string_list.append(word1[counter])
                string_list.append(word2[counter])
                counter+=1

            while counter < A:
                string_list.append(word1[counter])
                counter+=1

            while counter < B:
                string_list.append(word2[counter])
                counter+=1
            return ''.join(string_list)

### Time and Space Complexity

The time complexity of this approach is O(max(m, n)), where m and n are the lengths of word1 and word2. This is because each character from both strings is processed once. The space complexity is also O(m + n) since the final merged string contains all characters from both inputs.


## 3. Roman to Integer

### Problem Overview
The Roman to Integer problem requires us to take a string made up of Roman numeral characters and convert it into its corresponding integer value. Roman numerals were used in ancient Rome and are built using specific letters that represent fixed values. The challenge lies in not only interpreting each symbol but also understanding when to subtract values instead of adding them.

### Understanding Roman Numerals
There are seven Roman numeral symbols, each associated with a specific integer: I is 1, V is 5, X is 10, L is 50, C is 100, D is 500, and M is 1000. In most cases, you add the values of these symbols from left to right. For example, the numeral "VIII" is read as 5 + 1 + 1 + 1 = 8.

However, Roman numerals also allow for a subtractive notation. This occurs when a smaller numeral appears before a larger one, indicating that the smaller value should be subtracted from the larger. For instance, "IV" is 4, because 1 comes before 5, and "IX" is 9, because 1 comes before 10. This rule applies specifically to six cases: "IV" (4), "IX" (9), "XL" (40), "XC" (90), "CD" (400), and "CM" (900).

### Solution

    def romanToInt(self, s: str) -> int:
            d = {'I': 1, 'V':5, 'X':10, 'L':50, 'C':100, 'D': 500, 'M':1000}
            summ = 0
            n = len(s)
            i = 0

            while i < n:
                if i < n-1 and d[s[i]] < d[s[i+1]]:
                    summ += d[s[i+1]] - d[s[i]]
                    i+=2
                else:
                    summ += d[s[i]]
                    i+=1
            return summ


### Space and Time Complexity

The algorithm runs in linear time relative to the length of the input string, so the time complexity is O(n). This is because each character is processed at most once. The space complexity is O(1), since the character-to-value mapping is fixed and constant, and no additional data structures grow with input size.


## 4. Is Subsequence

### Problem Overview

The “Is Subsequence” problem is a popular coding question found on platforms like LeetCode. It asks whether a given string s is a subsequence of another string t. A subsequence is a series of characters that appear in the same relative order, but not necessarily contiguously. For example, the string "abc" is a subsequence of "ahbgdc", because the characters a, b, and c appear in the correct order, even though there are other characters in between.

### Solution

def isSubsequence(self, s: str, t: str) -> bool:
        S = len(s)
        T = len(t)
        if s == '': return True
        if S > T : return False
        
        j = 0

        for i in range(T):
            if t[i] == s[j]: # checking if the character in t matches character in s
                if j == S - 1: # checking if we have reached the last character of substring
                    return True
                j +=1 # increase the pointer j by 1

        return False

### Time and Space Complexity
This algorithm runs in O(n) time, where n is the length of t. We only scan through each character of t once. The space complexity is O(1) since we don’t use any additional data structures beyond a few variables.


## 5. Best Time to Buy and Sell Stock

### Problem Overview
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

### Solution

if done using brute force approach the time complexity is O(n^2)
we can solve this problem using greedy approach by scanning the sequence in one pass tracking the minimum price

    def maxProfit(self, prices: List[int]) -> int:
        max_profit = 0
        min_price = prices[0]
        for price in prices:
            if price < min_price:
                min_price = price
            profit = price - min_price
            if profit > max_profit:
                max_profit = profit
        return max_profit

### Time and Space Complexity
Time Complexity: O(n), where n is the length of the prices array. We make only a single pass through the array.
Space Complexity: O(1), since we use only two variables: min_price and max_profit.


## 6. Longest common prefix

### Problem statement

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

The “Longest Common Prefix” problem is a classic string processing task that asks you to find the longest starting substring that is shared among all strings in a given array. In simpler terms, given an array of strings, you are asked to return the common portion that all strings begin with. For example, given ["flower", "flow", "flight"], the longest common prefix is "fl", because it is the shared start of all the strings. If no common prefix exists, the correct result is an empty string "".

### Solution

        def longestCommonPrefix(self, strs: List[str]) -> str:
        min_length = float(inf)
        for s in strs:
            if len(s) < min_length:
                min_length = len(s)
        i = 0
        while i < min_length:
            for s in strs:
                if s[i] != strs[0][i]:
                    return s[:i]
            i = i+1
        return s[:i]

### Time and Space Complexity

Time complexity = O(n*m) n is number of string in the list and m is the minimum length of string 
Space complexity = O(1)

## 7. Summary ranges

### Problem Statement
The “Summary Ranges” problem asks us to process a sorted array of unique integers and return a compact list of string representations of all consecutive ranges. Each range should be expressed in the form "a->b" if a sequence exists, or just "a" if it stands alone.

For example, given the input [0, 1, 2, 4, 5, 7], the output should be ["0->2", "4->5", "7"]. This output represents three distinct segments of consecutive numbers compacted into human-readable strings.

### Solution

    def summaryRanges(self, nums: List[int]) -> List[str]:
        ans = []
        i = 0
        
        while i < len(nums):
            start = nums[i]

            while i < len(nums)-1 and nums[i]+1 == nums[i+1]:
                i = i +1
            
            if start==nums[i]:
                ans.append(str(nums[i]))
            else:
                ans.append(str(start)+"->"+str(nums[i]))
            i = i + 1
        return ans

### Time and Space Complexity
time = O(n)
spave O(1)

## 8. Product of array except itself

### Problem Statement

Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

 

Example 1:

Input: nums = [1,2,3,4]
Output: [24,12,8,6]


### Solution

    def productExceptSelf(self, nums: List[int]) -> List[int]:
            n = len(nums)
            l_mult = 1
            r_mult = 1

            l_arr = [0] * n
            r_arr = [0] * n
            print (l_arr)

            for i in range(n):
                j = -i-1
                l_arr[i] = l_mult
                r_arr[j] = r_mult
                l_mult *= nums[i]
                r_mult *= nums[j]

            return [l*r for l, r in zip(l_arr, r_arr)]     

### Time and space complexity
Time = 0(n)
Space = 0(n)