---
title: "序列化二叉树"
date: 2019-03-06T19:23:03+08:00
draft: false
categories: ["剑指offer"]
tags: ["Offer"]
---

### 题目描述

请实现两个函数，分别用来序列化和反序列化二叉树

#### 题解

```c++
#include <iostream>
#include <string>

using namespace std;

struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;

    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }

    TreeNode() {}
};

TreeNode *newTree() {
    TreeNode *node = new TreeNode;
    int x;
    cin >> x;
    if (!x)node = NULL;
    else {
        node->val = x;
        node->left = newTree();
        node->right = newTree();
    }
    return node;
}

void preOrder(TreeNode *pRoot)
{
    if (pRoot)
    {
        cout << pRoot->val << " ";
        preOrder(pRoot->left);
        preOrder(pRoot->right);
    }
}

char* Serialize(TreeNode *root) {
    if(!root)return "#";
    string s=to_string(root->val);
    s.push_back(',');
    char *left = Serialize(root->left);
    char *right = Serialize(root->right);
    char *res = new char[strlen(left) + strlen(right) + s.size()];
    strcpy(res, s.c_str());
    strcat(res, left);
    strcat(res, right);
    return res;
}

TreeNode* decode(char *&str) {
    if(*str=='#'){
        str++;
        return NULL;
    }
    int num = 0;
    while(*str != ',')
        num = num*10 + (*(str++)-'0');
    str++;
    TreeNode *root = new TreeNode(num);
    root->left = decode(str);
    root->right = decode(str);
    return root;
}

TreeNode* Deserialize(char *str) {
    return decode(str);
}

int main() {
    ios::sync_with_stdio(false);
    TreeNode *root = NULL;
    root = newTree();
    cout<<Serialize(root)<<endl;
    TreeNode * res = Deserialize(Serialize(root));
    preOrder(res);
    return 0;
}
```