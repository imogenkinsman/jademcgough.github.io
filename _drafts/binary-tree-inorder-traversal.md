---
layout: post
title: LeetCode - Binary Tree Inorder Traversal
---

Problem: [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/description/)

Nothing exciting to talk about here.

```c++
  vector<int> inorderTraversal(TreeNode* root) {
    vector<int> values;
    if (root) {
      vector<int> left = inorderTraversal(root->left);
      values.insert(end(values), begin(left), end(left));
      values.push_back(root->val);
      vector<int> right = inorderTraversal(root->right);
      values.insert(end(values), begin(right), end(right));
    }
    return values;
  }
```

The question also challenges you to solve it iteratively. Sure!

```c++

```
