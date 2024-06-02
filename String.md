# String
A string is an array of characters with other APIs and algorithms for manipulating strings, which means many array algorithms are also heavily used in strings, such as two-pointers and the sliding window.

While finding substrings, try the sliding window since it's good at finding sub-things. While finding unique or without repeating strings, try hashmap, for sure.

## Reverse String
[Like the linked list](https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/blob/master/LinkedList.md#206-reverse-linked-list), reversing is always a good test of our familiarity with a data structure. In this simple case, we use two-pointers as well.

[344. Reverse String](https://leetcode.com/problems/reverse-string/)
```js
const reverseString = (s) => {
    let left = 0
    let right = s.length - 1
    while (left < right) {
        [s[left], s[right]] = [s[right], s[left]]
        left++
        right--
    }
};
```

## Pattern Matching
Another big topic for string is pattern matching, aka finding if a string exists in another string. Of course, we can use two loops to compare each character, but it'll be O(m+n). That's why we have the KMP algorithm.

The time complexity is O(m+n) because we start over from the first character every time we mismatch. What if we don't have to start from the first character? The mismatch index is after a suffix, so if there is an equivalent prefix and we want to start over, we can start from the index after that prefix since the prefix and the suffix are equal and already matched. That's the KMP algorithm.

[28. Find the Index of the First Occurrence in a String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)
```js
const strStr = (haystack, needle) => {
    if (!needle.length) return 0;
    const getNext = (needle) => {
        let next = [0];
        let j = 0;
        for (let i = 1; i < needle.length; i++) {
            while (j > 0 && needle[i] !== needle[j])
                j = next[j - 1]
            if (needle[i] === needle[j])
                j++
            next.push(j)
        }
        return next
    }
    const next = getNext(needle)
    let j = 0
    for (let i = 0; i < haystack.length; i++) {
        while (j > 0 && haystack[i] !== needle[j])
            j = next[j - 1]
        if (haystack[i] === needle[j])
            j++
        if (j === needle.length)
            return i - needle.length + 1
    }
    return -1
};
```
