# Hash Map
Hash map collects data with key-value structures: one key, one data, one by one, that's why it usually costs O(1) to solve the problem. It's useful when checking if something exists in a collection, but it costs extra memory space. Array, set, and map are all hash maps. 

Since it has a key-value structure, the key to problem-solving usually is: which data to be the key, which data to be the value, and what's the relationship between these two? By making a good decision about that key, we solve almost every hash map problem.

## Map as hash map
The map is a classic type of hash map: one key, one value.

[454. 4Sum II](https://leetcode.com/problems/4sum-ii/)
```js
const fourSumCount = (nums1, nums2, nums3, nums4) => {
    const map = new Map()
    let count = 0
    for (const n1 of nums1) {
        for (const n2 of nums2) {
            const sum = n1 + n2
            map.set(sum, (map.get(sum) || 0) + 1)
        }
    }
    for (const n3 of nums3) {
        for (const n4 of nums4) {
            const sum = n3 + n4
            count += (map.get(0 - sum) || 0)
        }
    }
    return count
};
```

## Array as hash map
The array can be a hashmap since it has indexes as keys. It uses memory more efficiently than the set or map and could be more concise in some situations, which could be too far sometimes, however.

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

## Set as hash map
The set is like an array with no duplicates. JavaScript has a built-in constructor for set, which can take an array as a parameter, making it easy to use. However, it's slower and costs more memory space. And since it doesn't have an index, it can't collect two data like the array or map.

[349. Intersection of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays/)
```js
const intersection = (nums1, nums2) => {
    if (nums1.length < nums2.length) [nums1, nums2] = [nums2, nums1]
    const set1 = new Set(nums1)
    const res = new Set()
    for (const n of nums2) set1.has(n) && res.add(n)
    return Array.from(res)
};
```

## Try two-pointers
The hash map and two-pointers both collect two things, so sometimes, hash map problems can also be solved by two-pointers, especially when the array is sorted. In addition, two-pointers may be the better solution because it doesn't cost extra memory space, although the code may be a little harder to understand.

[167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum/description/)
```js
const twoSum = (numbers, target) => {
    // Using two pointers.
    let left = 0
    let right = numbers.length - 1
    while (left < right) {
        const sum = numbers[left] + numbers[right]
        if (sum === target) return [left + 1, right + 1]
        else if (sum < target) left++
        else right--
    }
    return []
    // Using a map.
    // const map = new Map()
    // for (let i = 0; i < numbers.length; i++) {
    //     const diff = target - numbers[i]
    //     if (map.has(diff)) return [map.get(diff) + 1, i + 1]
    //     map.set(numbers[i], i)
    // }
    // return []    
};
```
