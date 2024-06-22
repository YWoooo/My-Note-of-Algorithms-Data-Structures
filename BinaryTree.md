# Binary Tree
## Traversal the binary tree
### DFS
- Preorder
    ```js
    const preorderTraversal = (root) => {
      // Recursion
      const res = []
      const dfs = (root) => {
          if (!root) return null
          res.push(root.val)
          dfs(root.left)
          dfs(root.right)
      }
      dfs(root)
      return res
  
      // Iteration
      const res = []
      if (!root) return res
      const stack = [root]
      let curr = null
      while (stack.length) {
          curr = stack.pop()
          res.push(curr.val)
          curr.right && stack.push(curr.right)
          curr.left && stack.push(curr.left)
      }
      return res
  };
    ```
- Inorder
  ```js
  const postorderTraversal = (root) => {
    // Recursion
    const res = []
    const dfs = (root) => {
        if (!root) return
        dfs(root.left)
        dfs(root.right)
        res.push(root.val)
    }
    dfs(root)
    return res
  
    // Iteration
    const res = []
    if (!root) return res
    const stack = [root]
    let curr = null
    while (stack.length) {
        curr = stack.pop()
        res.push(curr.val)
        curr.left && stack.push(curr.left)
        curr.right && stack.push(curr.right)
    }
    return res.reverse()
  };
  ```
- Postorder
  ```js
  const inorderTraversal = (root) => {
    // Recursion
    const res = []
    const dfs = (root) => {
        if (!root) return
        dfs(root.left)
        res.push(root.val)
        dfs(root.right)
    }
    dfs(root)
    return res

    // Iteration
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
- Iteration only
