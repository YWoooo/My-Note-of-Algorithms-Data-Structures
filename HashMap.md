# Hash Map
Hash map collects data with key-value structures: one key, one data, one by one, which usually costs O(1) to solve the problem. It's useful when checking if something exists in a collection, but it costs extra memory space. The array, set, and map are all hash maps. 

## Using array as hash map
The array can be a hashmap since it has numbers as keys. It uses memory more efficiently than a set or map and could be more concise in some situations, which could be too far sometimes, however.

[242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
```js
const isAnagram = (s, t) => {
    if (s.length !== t.length) return false
    const hashmap = new Array(26).fill(0)
    const base = 'a'.charCodeAt()
    for (const i of s) hashmap[i.charCodeAt() - base]++
    for (const i of t) {
        if (!hashmap[i.charCodeAt() - base]) return false
        hashmap[i.charCodeAt() - base]--
    }
    return true
};
```

## Using set as hash map
## Using map as hash map
