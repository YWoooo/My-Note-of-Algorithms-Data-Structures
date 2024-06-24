# Binary Tree
## Traversal the binary tree
### DFS
#### Recursive
```js
const recursive = (root) => {
  const res = []
  const dfs = (root) => {
    if (!root) return null
    
    // Preorder
    res.push(root.val)
    dfs(root.left)
    dfs(root.right)
    
    // Inorder
    dfs(root.left)
    res.push(root.val)
    dfs(root.right)
    
    // Postorder
    dfs(root.left)
    dfs(root.right)
    res.push(root.val)
  }
  dfs(root)
  return res
};
```
#### Iterative
```js
const iterativePreorderAndPostorder = (root) => {
  const res = []
  if (!root) return res
  const stack = [root]

  // Preorder
  while (stack.length) {
    const curr = stack.pop()
    res.push(curr.val)
    curr.right && stack.push(curr.right)
    curr.left && stack.push(curr.left)
  }
  return res

  // Postorder
  while (stack.length) {
    const curr = stack.pop()
    res.push(curr.val)
    curr.left && stack.push(curr.left)
    curr.right && stack.push(curr.right)
  }
  return res.reverse()
}
const iterativeInorder = (root) => {
  const res = []
  const stack = []
  let curr = root
  while (stack.length || curr) {
    if (curr) {
      stack.push(curr)
      curr = curr.left
    } else {
      curr = stack.pop()
      res.push(curr.val)
      curr = curr.right
    }
  }
  return res
};
```
### BFS
#### Iteration only
```js
const bfs = (root) => {
  const res = []
  const queue = [root]
  if (!root) return res
  while (queue.length) {
    let length = queue.length
    const currLevel = []
    while (length--) {
      const node = queue.shift()
      currLevel.push(node.val)
      node.left && queue.push(node.left)
      node.right && queue.push(node.right)
    }
    res.push(currLevel)
  }
  return res
};
```
