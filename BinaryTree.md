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
  - Iteration
- Inorder
  - Recursion
  - Iteration
- Postorder
  - Recursion
  - Iteration
### BFS
- Iteration only
