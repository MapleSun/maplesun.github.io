---
title: Tree
date: 2018-06-15 15:51:49
tags:
---
## Basic
pre in post

Graph -> Tree:
* DFS: preorder inorder postorder
    * 实现方式： 
        1. 递归：DFS
        2. 迭代：Stack
* BFS: level order

### Thinking Tree Problem
1. 遍历方式
2. 实现方式
3. 套模板


### 模板
|----|特点|实现|
Preorder 通用解法  DFS
Inorder BST Stack & DFS
Postorder 子模块 DFS
Level order 层扫 BFS


#### Preorder 模板
* 通用解法
``` Java
public static void helper(List<Integer> res, TreeNode root) {
    if (root == null) return;
    // operation
    // 终止条件
    helper(res, root.left);
    helper(res, root.right);
}

```

* 双Preorder
``` Java
public boolean hasPathSum(TreeNode root, int sum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) {
        return sum == root.val;
    }

    return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
}
```
#### Inorder 模板
* 二叉搜索树： DFS & Stack
```Java
public static void helper(List<Integer> res, TreeNode root) {
    if (root == null) return;
    helper(res, root.left);
    // operation
    helper(res, root.right);
}

```

#### Level Order 模板
```Java
public static List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer> res = new ArrayList<>();
    if(root == null) return res;
    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    while(!queue.isEmpty()) {
        int size = queue.size();
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            TreeNode cur = queue.poll();
            if (cur.left != null) queue.offer(cur.left);
            if (cur.right != null) queue.offer(cur.right);
            list.add(cur.val);
        }
        res.add(list);
    }
    return res;
}
```

* DFS 实现 BFS - Level Order 模板
``` Java
public static void helper(List<List<Integer>> res, TreeNode root, int level) {
    if (root == null) return;
    if (level >= res.size()) {
        res.add(new ArrayList<>());
    }
    res.get(level).add(root.val);
    helper(res, root.left, level + 1);
    helper(res, root.right, level + 1);
}
```

### 综合
* DFS - Backtracking 
* Binary Search
* Graph - Union Find
* DP

## Skill
## LeetCode Question
## Interview Question