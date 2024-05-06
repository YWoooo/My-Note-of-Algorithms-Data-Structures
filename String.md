# String
A string is an array of characters with other APIs for manipulating strings, which means many array algorithms are also valuable for strings, such as two-pointers.

## Reverse String
[Like the linked list](https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/blob/master/LinkedList.md#206-reverse-linked-list), reversing is always a good test of our familiarity with a data structure. In this case, we use two-pointers as well.

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
