Leetcode [116. 填充每个节点的下一个右侧节点指针](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)

![img](https://assets.leetcode.com/uploads/2019/02/14/116_sample.png)

评论区解法：

```c++
class Solution {
public:
    Node* connect(Node* root) {
        if(root==NULL||root->left==NULL){
            return root;
        }
        else{
            root->left->next=root->right;
            if(root->next!=NULL){
            root->right->next=root->next->left;
            }
        }

        connect(root->left);
        connect(root->right);
        return root;
        
    }
};
```



非常有意思的解法。

对每一个节点来说，如果存在同辈节点，要做的事有两种：

跟自己的兄弟链接；

跟自己的堂兄弟链接；

作者把他转化为了：

对于一个父节点：

如果没孩子，什么也不做；

如果有孩子，先把孩子之间进行链接，再把孩子和侄子进行链接；



如何判断自己有孩子？

```c++
root->left==NULL
```

如何判断自己有兄弟？

```c++
root->next!=NULL
```



这一切的前提是：

父节点判定的优先级大于兄弟节点判定的优先级。

即：我有侄子的前提是我的父节点有儿子（完全二叉树意味着孩子数量等于且仅等于2）