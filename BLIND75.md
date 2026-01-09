# LeetCode Blind 75 - TypeScript

![Bidur Sapkota](https://www.bidursapkota.com.np/images/gravatar.webp "Bidur Sapkota - Developer")&nbsp;[Bidur Sapkota](https://www.bidursapkota.com.np/)

![Leetcode Blind 75 by Bidur Sapkota](/test.webp "Leetcode Blind 75 – Blog by Bidur Sapkota")

## Table of Contents

- [Arrays & Hashing](#arrays--hashing)
  - [Contains Duplicate](#contains-duplicate)
- [Two Pointers](#two-pointers)
  - [Valid Palindrome](#valid-palindrome)
- [Sliding Window](#sliding-window)
  - [Best Time to Buy and Sell Stock](#best-time-to-buy-and-sell-stock)
- [Stack](#stack)
  - [Valid Parentheses](#valid-parentheses)
- [Linked List](#linked-list)
  - [Reverse Linked List](#reverse-linked-list)

## Arrays & Hashing

### Contains Duplicate

Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

You should aim for a solution with O(n) time and O(n) space, where n is the size of the input array.

**Example 1**

```text
Input: nums = [1, 2, 3, 1];
Output: true;

Explanation:
The element 1 occurs at the indices 0 and 3.
```

**Example 2**

```text
Input: nums = [1,2,3,4]
Output: false

Explanation:
All elements are distinct.
```

**Solution**

We can use a **hash set** to efficiently keep track of the values we have already encountered.

As we iterate through the array, we check whether the current value is already present in the set.
If it is, that means we've seen this value before, so a duplicate exists.

Using a hash set allows constant-time lookups, making this approach much more efficient than comparing every pair.

**Algorithm**

1. Initialize an empty hash set to store seen values.
2. Iterate through each number in the array.
3. For each number:

   1. If it is already in the set, return True because a duplicate has been found.
   2. Otherwise, add it to the set.

4. If the loop finishes without finding any duplicates, return False.

```ts
function containsDuplicate(nums: number[]): boolean {
  const seen = new Set();
  for (let num of nums) {
    if (seen.has(num)) return true;
    seen.add(num);
  }
  return false;
}
```

**Time & Space Complexity**

- Time complexity: O(n)
- Space complexity: O(n)

## Two Pointers

### Valid Palindrome

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Note: Alphanumeric characters consist of letters (A-Z, a-z) and numbers (0-9).

You should aim for a solution with O(n) time and O(1) space, where n is the length of the input string.

**Example 1:**

```text
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Example 2:**

```text
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.
```

**Solution**

One pointer starts at the beginning (l) and the other at the end (r).

We move both pointers inward, skipping any characters that are not letters or digits.

Whenever both pointers point to valid characters, we compare them in lowercase form.

If at any point they differ, the string is not a palindrome.

This method avoids extra space and keeps the logic simple and efficient.

**Algorithm**

1. Initialize two pointers:
   - l at the start of the string,
   - r at the end of the string.
2. While l is less than r:
   - Move l forward until it points to an alphanumeric character.
   - Move r backward until it points to an alphanumeric character.
   - Compare the lowercase characters at l and r:
     - If they don’t match, return false.
   - Move both pointers inward: l += 1, r -= 1.
3. If the loop finishes without mismatches, return true.

```ts
function isPalindrome(s: string): boolean {
  let l = 0,
    r = s.length - 1;

  while (l < r) {
    while (l < r && !isAlphaNum(s[l])) l++;
    while (r > l && !isAlphaNum(s[r])) r--;
    if (s[l].toLowerCase() !== s[r].toLowerCase()) return false;

    l++;
    r--;
  }
  return true;
}

function isAlphaNum(c: string): boolean {
  return (
    (c >= "a" && c <= "z") || (c >= "A" && c <= "Z") || (c >= "0" && c <= "9")
  );
}
```

**Time & Space Complexity**

- Time complexity: O(n)
- Space complexity: O(1)

## Sliding Window

### Best Time to Buy and Sell Stock

**Example 1:**

```text
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

**Example 2:**

```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

You should aim for a solution with O(n) time and O(1) space, where n is the size of the input array.

**Solution**

As we scan through the prices, we keep track of two things:

1.  The lowest price so far → this is the best day to buy.
2.  The best profit so far → selling today minus the lowest buy price seen earlier.

At each price, we imagine selling on that day.
The profit would be:
`current price – lowest price seen so far`

We then update:

- the maximum profit,
- and the lowest price if we find a cheaper one.

This way, we make the optimal buy–sell decision in one simple pass.

**Algorithm**

1. Initialize:
   - minBuy as the first price,
   - maxP = 0 for the best profit.
2. Loop through each price sell:
   - Update maxP with sell - minBuy.
   - Update minBuy if we find a smaller price.
3. Return maxP after scanning all days.

```ts
function maxProfit(prices: number[]): number {
  let maxProfit = 0;
  let minBuy = prices[0];

  for (let sell of prices) {
    maxProfit = Math.max(maxProfit, sell - minBuy);
    minBuy = Math.min(minBuy, sell);
  }
  return maxProfit;
}
```

**Time & Space Complexity**

- Time complexity: O(n)
- Space complexity: O(1)

## Stack

### Valid Parentheses

Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.

Return true if s is a valid string, and false otherwise.

**Example 1:**

```text
Input: s = "()[]{}"
Output: true
```

**Example 2:**

```text
Input: s = "([)]"
Output: false
```

You should aim for a solution with O(n) time and O(n) space, where n is the length of the given string.

**Solution**

Valid parentheses must follow a last-opened, first-closed order — just like stacking plates.

So we use a stack to track opening brackets.

Whenever we see a closing bracket, we simply check whether it matches the most recent opening bracket on top of the stack.

If it matches, we remove that opening bracket.

If it doesn’t match (or the stack is empty), the string is invalid.

A valid string ends with an empty stack.

**Algorithm**

1. Create a stack to store opening brackets.
2. For each character in the string:
   - If it is an opening bracket, push it onto the stack.
   - If it is a closing bracket:
     - Check if the stack is not empty and its top matches the corresponding opening bracket.
     - If yes, pop the stack.
     - Otherwise, return false.
3. After processing all characters:
   - If the stack is empty, return true.
   - Otherwise, return false.

```ts
function isValid(s: string): boolean {
  const stack: string[] = [];
  const closeToOpen = {
    ")": "(",
    "}": "{",
    "]": "[",
  };

  for (let c of s) {
    if (closeToOpen[c]) {
      if (stack.length > 0 && stack[stack.length - 1] === closeToOpen[c])
        stack.pop();
      else return false;
    } else stack.push(c);
  }
  return stack.length === 0;
}
```

**Time & Space Complexity**

- Time complexity: O(n)
- Space complexity: O(n)

## Linked List

### Reverse Linked List

Given the head of a singly linked list, reverse the list, and return the reversed list.

**Example 1:**

```text
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```

**Example 2:**

```text
Input: head = []
Output: []
```

You should aim for a solution with O(n) time and O(1) space, where n is the length of the given list.

Reversing a linked list iteratively is all about flipping pointers one step at a time.

We walk through the list from left to right, and for each node, we redirect its next pointer to point to the node behind it.

To avoid losing track of the rest of the list, we keep three pointers:

- curr → the current node we are processing
- prev → the node that should come after curr once reversed
- temp → the original next node (so we don’t break the chain)

By moving these pointers forward in each step, we gradually reverse the entire list.

When curr becomes None, the list is fully reversed, and prev points to the new head.

**Algorithm**

1. Initialize:

   - prev = None
   - curr = head

2. While curr exists:

   - Save the next node: temp = curr.next
   - Reverse the pointer: curr.next = prev
   - Move prev to curr
   - Move curr to temp

3. When the loop ends, prev is the new head of the reversed list.
4. Return prev.

```ts
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList(head: ListNode | null): ListNode | null {
  let prev = null,
    curr = head,
    temp = null;
  while (curr) {
    temp = curr.next;
    curr.next = prev;
    prev = curr;
    curr = temp;
  }
  return prev;
}
```

**Time & Space Complexity**

Time complexity: O(n)
Space complexity: O(1)
