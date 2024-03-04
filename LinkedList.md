# Linked List
Like the [array](https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/blob/master/Array.md), the linked list collects the same data type. The difference is the array stores data in continuous memory space, but the linked list stores data separately, connecting data with pointers. A typical node of a linked list looks like this.
```js
function ListNode(val, next) {
    this.val = val ?? 0
    this.next = next ?? null
}
```
The while loop and [two-pointers](https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/blob/master/Array.md#two-pointers) can solve many linked list problems.

## Basic CRUD
The linked list is not a built-in data structure, at least in JavaScript. So the interview problems with the linked list are more about some manipulations, such as basic CRUD, or a little bit advanced, fancier ones. If we memorize them well, they won't be hard at all.

### [203. The Dummy Head](https://leetcode.com/problems/remove-linked-list-elements/description/)
Before we talk about the CRUD of the linked list, it will be much easier if we learn a technique called the dummy head. Operating a node of a linked list relates to the previous and the next nodes. And since the head node doesn't have a previous node, we need a specific logic to handle it, making our code chunky.

So we can add a dummy head node to the linked list. By doing this, all other nodes have the previous and the next nodes. No specific logic is needed.

```js
const removeElements = (head, val) => {
    const dummyHead = new ListNode(0, head)
    let curr = dummyHead
    while (curr.next) {
        if (curr.next.val === val) {
            curr.next = curr.next.next
            continue
        }
        curr = curr.next
    }
    return dummyHead.next
};
```

### [707. The CRUD](https://leetcode.com/problems/design-linked-list/description/)
After learning the dummy head, the CRUD of the linked list will be much easier.  

```js
class LinkedNode {
    constructor(val, next) {
        this.val = val;
        this.next = next;
    }
}
var MyLinkedList = function() {
    this.dummyHead = new LinkedNode(0)
    this.size = 0;
    this.tail = null;
    this.head = null;
};
MyLinkedList.prototype.get = function(index) {
    if (index > this.size - 1 || index < 0) return -1
    let curr = this.dummyHead.next
    while (index--) curr = curr.next
    return curr.val
};
MyLinkedList.prototype.addAtHead = function(val) {
    newNode = new LinkedNode(val)
    newNode.next = this.dummyHead.next
    this.dummyHead.next = newNode
    this.size++
};
MyLinkedList.prototype.addAtTail = function(val) {
    let newNode = new LinkedNode(val)
    let curr = this.dummyHead
    while (curr.next) curr = curr.next
    curr.next = newNode
    this.size++
};
MyLinkedList.prototype.addAtIndex = function(index, val) {
    if (index > this.size) return
    if (index < 0) index = 0
    let newNode = new LinkedNode(val)
    let curr = this.dummyHead
    while (index--) curr = curr.next
    newNode.next = curr.next
    curr.next = newNode
    this.size++
};
MyLinkedList.prototype.deleteAtIndex = function(index) {
    if (index >= this.size || index < 0) return
    let curr = this.dummyHead
    while (index--) curr = curr.next
    curr.next = curr.next.next
    this.size--
};
```
### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
It's not hard, but interviewers love this problem. Just loop through, reverse, and move pointers.

```js
// Two pointer.
const reverseList = (head) => {
    let curr = head
    let pre = null
    while (curr) {
        const temp = curr.next
        // Reverse.
        curr.next = pre
        // Move pointers.
        pre = curr
        curr = temp
    }
    return pre
};

// Recursion.
const reverseList = (head) => {
    const reverse = (pre, head) => {
        if (!head) return pre
        const temp = head.next
        // Reverse.
        head.next = pre
        // Move pointers.
        pre = head
        return reverse(pre, temp)
    }
    return reverse(null, head)
}
```

### [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/)
Use two pointers and a current pointer. It isn't hard at all, and it's a good practice for basic linked list operations.

```js
const mergeTwoLists = (list1, list2) => {
    const dummyHead = new ListNode()
    let curr = dummyHead
    while (list1 && list2) {
        if (list1.val <= list2.val) {
            curr.next = list1
            list1 = list1.next
        } else {
            curr.next = list2
            list2 = list2.next
        }
        curr = curr.next
    }
    curr.next = list1 ?? list2
    return dummyHead.next
};
```

## Fancier CRUD

### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)
Using fast and slow pointers. And since using a dummy head, the fast pointer moves n + 1 steps initially, not just n. Some articles make this n or n + 1 part overcomplicated. Please don't be confused.
```js
const removeNthFromEnd = function(head, n) {
    const dummyHead = new ListNode(0, head)
    let slow = dummyHead
    let fast = dummyHead
    while (n--) fast = fast.next
    while (fast.next) {
        fast = fast.next
        slow = slow.next
    }
    slow.next = slow.next.next
    return dummyHead.next
};
```
### [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
Another fancier but surprisingly easier problem, which is just a combination of a few basic operations. Get the difference of lengths, move A with that difference, and we can compare.
```js
const getIntersectionNode = (headA, headB) => {
    const getLen = (head) => {
        let len = 0
        let curr = head
        while (curr) {
            curr = curr.next
            len++
        }
        return len
    }
    let currA = headA
    let currB = headB
    let lenA = getLen(headA)
    let lenB = getLen(headB)
    if (lenA < lenB) {
        // Always use semicolon while destructing arrays.
        // For example, without semicolons, these two lines equal to
        // [curA, curB] = [lenB, lenA].
        [currA, currB] = [currB, currA];
        [lenA, lenB] = [lenB, lenA];
    }
    let diff = lenA - lenB
    while (diff--) currA = currA.next
    while (currA && currA !== currB) {
        currA = currA.next
        currB = currB.next
    }
    return currA
};
```
### [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/)
Use fast and slow pointers to loop through. If they meet, there must be a cycle.

![image](https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/assets/46885342/bf581036-290f-4134-b740-2f1439ae1faf)


Once they meet, move a pointer to the head, starting over step by step. The node they meet again must be where the cycle begins since they move together, step by step. It's called [the Tortoise and Hare algorithm.](https://www.google.com/search?q=Tortoise+and+Hare+algorithm.&sourceid=chrome&ie=UTF-8)

<img width="300" src="https://github.com/YWoooo/My-Note-of-Algorithms-Data-Structures/assets/46885342/d5356058-3dbb-4e97-9393-21ee78faeef7">


```js
const detectCycle = function(head) {
    if (!head || !head.next) return null
    let slow = head.next
    let fast = head.next.next
    while (fast && fast.next) {
        slow = slow.next
        fast = fast.next.next
        if (fast === slow) {
            slow = head
            while (fast !== slow) {
                slow = slow.next
                fast = fast.next
            }
            return slow
        }
    }
    return null
};
```
### [143. Reorder List](https://leetcode.com/problems/reorder-list/)
It's just the combination of [reversing](#206-reverse-linked-list) and [merging](#21-merge-two-sorted-lists) the linked list.

```js
const reorderList = (head) => {
    if (!head || !head.next) return

    // Find the middle of the list.
    let slow = head
    let fast = head
    while (fast.next && fast.next.next) {
        slow = slow.next
        fast = fast.next.next
    }

    // Reverse the second half of the list.
    let prev = null
    let curr = slow.next
    while (curr) {
        let nextTemp = curr.next
        curr.next = prev
        prev = curr
        curr = nextTemp
    }
    slow.next = null

    // Merge the two lists.
    let first = head
    let second = prev
    while (second) {
        let temp1 = first.next
        let temp2 = second.next
        first.next = second
        second.next = temp1
        first = temp1
        second = temp2
    }
};
```
