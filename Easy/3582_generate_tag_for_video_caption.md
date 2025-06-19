# 3582. Generate Tag for Video Caption

**Difficulty:** Easy  
**Tags:** String, String Manipulation  
**Link:** [Leetcode 3582](https://leetcode.com/problems/generate-tag-for-video-caption/)

---

## 🔒 Problem Statement

You are given a string `caption` representing the caption for a video.

Generate a tag by applying the following steps:

1. Combine all words into a single **camelCase** string prefixed with `#`.
   - The first word is lowercase.
   - Capitalize the first letter of all subsequent words.

2. Remove all non-English letter characters (except the first `#`).

3. Truncate the result to a **maximum of 100 characters**.

Return the final tag string.

---

### 🧪 Examples

#### Example 1:
```
Input: caption = "Leetcode daily streak achieved"
Output: "#leetcodeDailyStreakAchieved"
```

#### Example 2:
```
Input: caption = "can I Go There"
Output: "#canIGoThere"
```

#### Example 3:
```
Input: caption = "hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh"
Output: "#hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh"
```

---

### ✅ Constraints

- `1 <= caption.length <= 150`
- `caption` consists of only English letters and spaces

---

## ✅ Solution

### 🔍 Approach

- **Step 1:** Split the string into words.
- **Step 2:** Build a camelCase string from the words.
- **Step 3:** Remove all non-letter characters.
- **Step 4:** Add `#` at the beginning and **truncate** to 100 characters if necessary.

---

### 👨‍💻 Python Code

```python
class Solution(object):
    def generateTag(self, caption):
        """
        :type caption: str
        :rtype: str
        """
        # Step 1: Split the caption into words
        words = caption.split()

        if not words:
            return "#"

        # Step 2: Create camelCase formatting
        camel_case = words[0].lower() + ''.join(word.capitalize() for word in words[1:])

        # Step 3: Remove non-letter characters (excluding the first '#')
        clean_tag = '#' + ''.join(char for char in camel_case if char.isalpha())

        # Step 4: Truncate to 100 characters
        return clean_tag[:100]
```

---

### ⏱️ Time & Space Complexity

- **Time Complexity:** `O(n)` where `n` is the length of the caption
- **Space Complexity:** `O(n)` for storing intermediate tag data

---

## 🧪 Submission Info

- **Status:** ✅ Accepted  
- **Language:** Python  
- **Runtime:** 6 ms (Beats 42.40%)  
- **Memory Usage:** 12.56 MB (Beats 13.31%)  
- **Submitted by:** Rajesh Kumar Jogi on Jun 19, 2025 at 17:39

---

## 🧠 Notes

- Handles long single-word captions by truncating to fit the 100 character limit.
- Works well for edge cases like empty strings, excessive spaces, and upper/lower case noise.

---
