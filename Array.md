# Array
Array collects the same type of data stored in continuous memory space, which means adding or removing elements usually costs a lot. There are some classic algorithms for arrays.

## Binary Search
Find the target value in the middle of a sorted array without duplicate. If not found, halve the left or right and repeat. Since the array is sorted and we start in the middle, we remove half the elements in each search, making it Olog(n).

The key s interval. We must stick with the definition of the interval we want, keeping it unchanged in every halving, or we will be struggling with these edge cases, such as `while(left < right)` or `while(left <= right)`? `right = middle` or `right = middle - 1`?

[704. Binary Search](https://leetcode.com/problems/binary-search/submissions/1147964083/)

```js
const binarySearch = (nums, target) => {
    let left = 0
    let right = nums.length - 1
    let mid = 0

    while (left <= right) {
        mid = left + Math.floor((right - left) / 2)
        if (nums[mid] > target) right = mid - 1
        else if (nums[mid] < target) left = mid + 1
        else return mid
    }
    return -1
}
```

## Two Pointers
Use two pointers to loop through an array. Since it has two pointers, it can do the job that usually needs two for-loop. The time complexity is O(n) and the space complexity could be O(1).

[27. Remove Element](https://leetcode.com/problems/remove-element/description/)

```js
const removeElement = function(nums, val) {
    let slow = 0
    for (let i = 0; i < nums.length; i++) {
        if (nums[i] !== val) nums[slow++] = nums[i]
    }
    return slow
};
```

## Sliding Window
The sliding window is just another two-pointer. By moving two pointers, we make a sliding window. The difference is that sliding-window is more like finding a subarray, but the two-pointer can find anything.

The key is what is inside the window and when to move the left pointer.

[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)

```js
const minSubArrayLen = function(target, nums) {
    let left = 0
    let right = 0
    let sum = 0
    let res = Infinity
    
    while (right < nums.length) {
        sum += nums[right];
        while (sum >= target) {
            res = Math.min(res, right - left + 1);
            sum -= nums[left];
            left++;
        }
        right++;
    }
    return res === Infinity ? 0 : res
};
```
