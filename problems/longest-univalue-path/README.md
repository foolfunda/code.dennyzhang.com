# Leetcode: Longest Univalue Path     :BLOG:Basic:


---

Longest Univalue Path  

---

Given a binary tree, find the length of the longest path where each node in the path has the same value. This path may or may not pass through the root.  

Note: The length of path between two nodes is represented by the number of edges between them.  

    Example 1:
    
    Input:
    
                  5
                 / \
                4   5
               / \   \
              1   1   5
    Output:
    
    2

    Example 2:
    
    Input:
    
                  1
                 / \
                4   5
               / \   \
              4   4   5
    Output:
    
    2

Note: The given binary tree has not more than 10000 nodes. The height of the tree is not more than 1000.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/longest-univalue-path)  

Credits To: [leetcode.com](https://leetcode.com/problems/longest-univalue-path/description/)  

Leave me comments, if you have better ways to solve.  

---

Related discussions: [here](https://leetcode.com/problems/longest-univalue-path/discuss/108155/C++-DFS-with-explanation)  

    ## Blog link: https://code.dennyzhang.com/longest-univalue-path
    
    # Definition for a binary tree node.
    # class TreeNode:
    #     def __init__(self, x):
    #         self.val = x
    #         self.left = None
    #         self.right = None
    
    class Solution:
        ## Basic Ideas: dfs
        ##
        ## Complexity:
        def longestUnivaluePath(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            if root is None: return 0
            # global variable for the longes path
            self.res = 1
            self.dfs(root)
            return self.res - 1
    
        def dfs(self, root):
            # get the longest path
            # return value is the longest path for one sub-tree
            ##           and the path value is the root value
            if root is None: return 0
            l = self.dfs(root.left)
            r = self.dfs(root.right)
    
            if not (root.left and root.left.val == root.val):
                l = 0
            if not (root.right and root.right.val == root.val):
                r = 0
    
            self.res = max(self.res, l+r+1)
            return max(l, r)+1
    
        ## Basic Ideas: recursive + BFS
        ##
        ## Complexity Time O(n*n), Space O(n)
        ##
        def longestUnivaluePath_v1(self, root):
            """
            :type root: TreeNode
            :rtype: int
            """
            if root is None: return 0
            # BFS
            import collections
            queue = collections.deque()
            queue.append(root)
            (l, r) = self.longestPath(root, root.val)
            res = l + r + 1
            while len(queue) != 0:
                for k in range(len(queue)):
                    node = queue.popleft()
                    # find candidates
                    if node.left:
                        (l, r) = self.longestPath(node.left, node.left.val)
                        res = max(res, l+r+1)
                        queue.append(node.left)
                    if node.right:
                        (l, r) = self.longestPath(node.right, node.right.val)
                        res = max(res, l+r+1)
                        queue.append(node.right)
            return res - 1
    
        def longestPath(self, root, val):
            # find the longest path which includes root, and the value is val.
            if root is None: return (0, 0)
            if root.val != val: return (0, 0)
            if root.left is None and root.right is None:
                return (0, 0)
    
            l, r = 0, 0
            if root.left and root.left.val == val:
                # choose one path
                l = max(self.longestPath(root.left, val))+1
            if root.right and root.right.val == val:
                # choose one path
                r = max(self.longestPath(root.right, val))+1
            return (l, r)