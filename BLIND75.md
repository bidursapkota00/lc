# LeetCode Blind 75 - TypeScript

![Bidur Sapkota](https://www.bidursapkota.com.np/images/gravatar.webp "Bidur Sapkota - Developer")&nbsp;[Bidur Sapkota](https://www.bidursapkota.com.np/)

![Leetcode Blind 75 by Bidur Sapkota](/test.webp "Leetcode Blind 75 – Blog by Bidur Sapkota")

## Table of Contents

- [Arrays & Hashing](#arrays--hashing)
  - [Contains Duplicate](#contains-duplicate)
- [Two Pointers](#two-pointers)
  - [Valid Palindrome](#valid-palindrome)

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
