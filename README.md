# sword-point-offer

《剑指offer》解题集，顺便学c++

题目都来自于牛客网的[剑指offer](https://www.nowcoder.com/ta/coding-interviews)题集，可以拷贝代码到相应题目上调试

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
- [sword-point-offer](#sword-point-offer)
  - [01 二维数组中的查找](#01-%E4%BA%8C%E7%BB%B4%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9F%A5%E6%89%BE)
    - [题目：](#%E9%A2%98%E7%9B%AE)
    - [思路：](#%E6%80%9D%E8%B7%AF)
    - [代码：](#%E4%BB%A3%E7%A0%81)
    - [调试](#%E8%B0%83%E8%AF%95)
  - [02 替换空格](#02-%E6%9B%BF%E6%8D%A2%E7%A9%BA%E6%A0%BC)
    - [题目：](#%E9%A2%98%E7%9B%AE-1)
    - [思路：](#%E6%80%9D%E8%B7%AF-1)
      - [背景：](#%E8%83%8C%E6%99%AF)
      - [方法：](#%E6%96%B9%E6%B3%95)
    - [代码：](#%E4%BB%A3%E7%A0%81-1)
    - [调试](#%E8%B0%83%E8%AF%95-1)
  - [03 从尾到头打印链表](#03-%E4%BB%8E%E5%B0%BE%E5%88%B0%E5%A4%B4%E6%89%93%E5%8D%B0%E9%93%BE%E8%A1%A8)
    - [题目：](#%E9%A2%98%E7%9B%AE-2)
    - [思路：](#%E6%80%9D%E8%B7%AF-2)
    - [代码：](#%E4%BB%A3%E7%A0%81-2)
      - [用递归实现代码](#%E7%94%A8%E9%80%92%E5%BD%92%E5%AE%9E%E7%8E%B0%E4%BB%A3%E7%A0%81)
      - [用栈实现代码](#%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E4%BB%A3%E7%A0%81)
    - [调试](#%E8%B0%83%E8%AF%95-2)
  - [04 重建二叉树](#04-%E9%87%8D%E5%BB%BA%E4%BA%8C%E5%8F%89%E6%A0%91)
    - [题目：](#%E9%A2%98%E7%9B%AE-3)
    - [思路：](#%E6%80%9D%E8%B7%AF-3)
    - [代码：](#%E4%BB%A3%E7%A0%81-3)
    - [调试](#%E8%B0%83%E8%AF%95-3)
  - [05 用两个栈实现队列](#05-%E7%94%A8%E4%B8%A4%E4%B8%AA%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97)
    - [题目](#%E9%A2%98%E7%9B%AE)
    - [思路](#%E6%80%9D%E8%B7%AF)
    - [代码](#%E4%BB%A3%E7%A0%81)
    - [调试](#%E8%B0%83%E8%AF%95-4)
  - [06 旋转数组的最小数字](#06-%E6%97%8B%E8%BD%AC%E6%95%B0%E7%BB%84%E7%9A%84%E6%9C%80%E5%B0%8F%E6%95%B0%E5%AD%97)
    - [题目：](#%E9%A2%98%E7%9B%AE-4)
    - [思路：](#%E6%80%9D%E8%B7%AF-4)
    - [代码](#%E4%BB%A3%E7%A0%81-1)
    - [调试](#%E8%B0%83%E8%AF%95-5)
  - [07 斐波那契数列](#07-%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97)
    - [题目：](#%E9%A2%98%E7%9B%AE-5)
    - [思路：](#%E6%80%9D%E8%B7%AF-5)
    - [代码](#%E4%BB%A3%E7%A0%81-2)
    - [调试](#%E8%B0%83%E8%AF%95-6)
  - [08 跳台阶](#08-%E8%B7%B3%E5%8F%B0%E9%98%B6)
    - [题目](#%E9%A2%98%E7%9B%AE-1)
    - [思路](#%E6%80%9D%E8%B7%AF-1)
    - [代码](#%E4%BB%A3%E7%A0%81-3)
    - [调试](#%E8%B0%83%E8%AF%95-7)
  - [09 变态跳台阶](#09-%E5%8F%98%E6%80%81%E8%B7%B3%E5%8F%B0%E9%98%B6)
    - [题目](#%E9%A2%98%E7%9B%AE-2)
    - [思路](#%E6%80%9D%E8%B7%AF-2)
    - [代码](#%E4%BB%A3%E7%A0%81-4)
      - [动态规划](#%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92)
      - [数学推导](#%E6%95%B0%E5%AD%A6%E6%8E%A8%E5%AF%BC)
    - [调试](#%E8%B0%83%E8%AF%95-8)
  - [10 矩形覆盖](#10-%E7%9F%A9%E5%BD%A2%E8%A6%86%E7%9B%96)
    - [题目](#%E9%A2%98%E7%9B%AE-3)
    - [思路](#%E6%80%9D%E8%B7%AF-3)
    - [代码](#%E4%BB%A3%E7%A0%81-5)
    - [调试](#%E8%B0%83%E8%AF%95-9)
  - [11 二进制中1的个数](#11-%E4%BA%8C%E8%BF%9B%E5%88%B6%E4%B8%AD1%E7%9A%84%E4%B8%AA%E6%95%B0)
    - [题目](#%E9%A2%98%E7%9B%AE-4)
    - [思路](#%E6%80%9D%E8%B7%AF-4)
    - [代码](#%E4%BB%A3%E7%A0%81-6)
    - [调试](#%E8%B0%83%E8%AF%95-10)
  - [12 数值的整数次方](#12-%E6%95%B0%E5%80%BC%E7%9A%84%E6%95%B4%E6%95%B0%E6%AC%A1%E6%96%B9)
    - [题目](#%E9%A2%98%E7%9B%AE-5)
    - [思路](#%E6%80%9D%E8%B7%AF-5)
    - [代码](#%E4%BB%A3%E7%A0%81-7)
    - [调试](#%E8%B0%83%E8%AF%95-11)
  - [13 调整数组顺序使奇数位于偶数前面](#13-%E8%B0%83%E6%95%B4%E6%95%B0%E7%BB%84%E9%A1%BA%E5%BA%8F%E4%BD%BF%E5%A5%87%E6%95%B0%E4%BD%8D%E4%BA%8E%E5%81%B6%E6%95%B0%E5%89%8D%E9%9D%A2)
    - [题目](#%E9%A2%98%E7%9B%AE-6)
    - [思路](#%E6%80%9D%E8%B7%AF-6)
    - [代码](#%E4%BB%A3%E7%A0%81-8)
    - [调试](#%E8%B0%83%E8%AF%95-12)
  - [14 链表中倒数第k个结点](#14-%E9%93%BE%E8%A1%A8%E4%B8%AD%E5%80%92%E6%95%B0%E7%AC%ACk%E4%B8%AA%E7%BB%93%E7%82%B9)
    - [题目](#%E9%A2%98%E7%9B%AE-7)
    - [思路](#%E6%80%9D%E8%B7%AF-7)
    - [代码](#%E4%BB%A3%E7%A0%81-9)
    - [调试](#%E8%B0%83%E8%AF%95-13)
  - [15 反转链表](#15-%E5%8F%8D%E8%BD%AC%E9%93%BE%E8%A1%A8)
    - [题目](#%E9%A2%98%E7%9B%AE-8)
    - [思路](#%E6%80%9D%E8%B7%AF-8)
    - [代码](#%E4%BB%A3%E7%A0%81-10)
    - [调试](#%E8%B0%83%E8%AF%95-14)
  - [16 合并两个排序的链表](#16-%E5%90%88%E5%B9%B6%E4%B8%A4%E4%B8%AA%E6%8E%92%E5%BA%8F%E7%9A%84%E9%93%BE%E8%A1%A8)
    - [题目](#%E9%A2%98%E7%9B%AE-9)
    - [思路](#%E6%80%9D%E8%B7%AF-9)
    - [代码](#%E4%BB%A3%E7%A0%81-11)
      - [递归](#%E9%80%92%E5%BD%92)
      - [迭代](#%E8%BF%AD%E4%BB%A3)
    - [调试](#%E8%B0%83%E8%AF%95-15)
  - [17 树的子结构](#17-%E6%A0%91%E7%9A%84%E5%AD%90%E7%BB%93%E6%9E%84)
    - [题目](#%E9%A2%98%E7%9B%AE-10)
    - [思路](#%E6%80%9D%E8%B7%AF-10)
    - [代码](#%E4%BB%A3%E7%A0%81-12)
    - [调试](#%E8%B0%83%E8%AF%95-16)
  - [18 二叉树的镜像](#18-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E9%95%9C%E5%83%8F)
    - [题目](#%E9%A2%98%E7%9B%AE-11)
    - [思路](#%E6%80%9D%E8%B7%AF-11)
    - [代码](#%E4%BB%A3%E7%A0%81-13)
    - [调试](#%E8%B0%83%E8%AF%95-17)
  - [19 顺时针打印矩阵](#19-%E9%A1%BA%E6%97%B6%E9%92%88%E6%89%93%E5%8D%B0%E7%9F%A9%E9%98%B5)
    - [题目](#%E9%A2%98%E7%9B%AE-12)
    - [思路](#%E6%80%9D%E8%B7%AF-12)
    - [代码](#%E4%BB%A3%E7%A0%81-14)
    - [调试](#%E8%B0%83%E8%AF%95-18)
  - [20 包含min函数的栈](#20-%E5%8C%85%E5%90%ABmin%E5%87%BD%E6%95%B0%E7%9A%84%E6%A0%88)
    - [题目](#%E9%A2%98%E7%9B%AE-13)
    - [思路](#%E6%80%9D%E8%B7%AF-13)
    - [代码](#%E4%BB%A3%E7%A0%81-15)
    - [调试](#%E8%B0%83%E8%AF%95-19)
  - [21 栈的压入、弹出序列](#21-%E6%A0%88%E7%9A%84%E5%8E%8B%E5%85%A5%E5%BC%B9%E5%87%BA%E5%BA%8F%E5%88%97)
    - [题目](#%E9%A2%98%E7%9B%AE-14)
    - [思路](#%E6%80%9D%E8%B7%AF-14)
    - [代码](#%E4%BB%A3%E7%A0%81-16)
    - [调试](#%E8%B0%83%E8%AF%95-20)
  - [22 从上往下打印二叉树](#22-%E4%BB%8E%E4%B8%8A%E5%BE%80%E4%B8%8B%E6%89%93%E5%8D%B0%E4%BA%8C%E5%8F%89%E6%A0%91)
    - [题目](#%E9%A2%98%E7%9B%AE-15)
    - [思路](#%E6%80%9D%E8%B7%AF-15)
    - [代码](#%E4%BB%A3%E7%A0%81-17)
    - [调试](#%E8%B0%83%E8%AF%95-21)
  - [23 二叉搜索树的后序遍历序列](#23-%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91%E7%9A%84%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97)
    - [题目](#%E9%A2%98%E7%9B%AE-16)
    - [思路](#%E6%80%9D%E8%B7%AF-16)
    - [代码](#%E4%BB%A3%E7%A0%81-18)
    - [调试](#%E8%B0%83%E8%AF%95-22)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## 01 二维数组中的查找

### 题目：

在一个二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。

请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

### 思路：

鉴于数组的规律性，选取数组查找范围的右上角数字，

如果与查找的数字相等， 则返回true；

如果比查找的数字大，则将该数字所在列从查找范围剔除；

如果比查找的数字小，则将该数字所在行从查找范围中剔除。


### 代码：

````c++
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int rows=array.size();
        int cols=array[0].size();
        int r=0,c=cols-1;
        while(r<rows && c>=0){
            if(target==array[r][c])
                return true;
            if(target<array[r][c])
                c--;
            else
                r++;
        }
        return false;
    }
};
````

### 调试

[二维数组中的查找](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e)

## 02 替换空格

### 题目：

请实现一个函数，把字符串中的每个空格替换成“%20”，例如输入“We are happy”,则输出“We%20are%20happy”。

### 思路：

#### 背景：

在网络编程中，如果URL参数中含有特殊字符，如空格，#等，导致服务器端无法获得正确的参数值，我们需要将这些特殊符号转换成服务器可以识别的字符。转换的规则就是在‘%’后面跟上ASCII码的两位十六进制的表示，比如空格的ASCII码是32，即十六进制的）0x20，因此空格被替换为“%20”。

#### 方法：

1. 假设可以开辟新的空间。

    　创建一新字符串，并在新字符串上面做空格替换。

    　时间复杂度：O(n)，空间复杂度：O(n)

2. 假设不能开辟新的空间，且原字符串长度足够。

    从头到尾扫描字符串，每遇到空格字符时做替换，将1个字符替换为3个字符，因此空格后面的字符需要后移两个字符。
    时间复杂度：O(n^2)，空间复杂度：O(0)

    从尾向头扫描字符串，每遇到空格字符时做替换，无需后移字符。首先遍历一遍字符串，统计字符串中空格的个数，并计算替换后字符串的总长度，每替换一个空格，长度增加2.替换时，准备两个指针P1，P2分别指向原始字符串的末尾和替换后字符串的末尾，依次移动指针P1，遇到空格做替换，直至P1和P2相遇，即前面不再有空格出现。
    时间复杂度：O(n)，空间复杂度：O(0)

### 代码：

以下代码是从尾向头扫描字符串
````c++
class Solution {
public:
    string replaceSpace(char *str,int length) {
        int originalLength=length;
        int numberOfBlank=0;
        int i=0;
        while(str[i]!='\0'){
            if(str[i]==' ')
                ++numberOfBlank;
            ++i;
        }
 
        int newLength=originalLength+numberOfBlank*2;
        int indexOfOriginal=originalLength;
        int indexOfNew=newLength;
        while(indexOfOriginal>=0 && indexOfNew>indexOfOriginal){
            if(str[indexOfOriginal]==' '){
                str[indexOfNew--]='0';
                str[indexOfNew--]='2';
                str[indexOfNew--]='%';
            }
            else
                str[indexOfNew--]=str[indexOfOriginal];
            --indexOfOriginal;
        }
        return str;
    }
};
````

### 调试

[替换空格](https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423)

## 03 从尾到头打印链表

### 题目：

输入一个链表的头结点，从尾到头反过来打印每个结点的值。

### 思路：

1. 使用栈，遍历整个链表，将结点依次入栈，然后再依次出栈，实现“后进先出”。
2. 递归实现,如果链表结点数过多的话，可能会导致栈溢出。

### 代码：

#### 用递归实现代码

````c++
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    void helper(ListNode* head,vector<int> &nodes){
        if(head!=NULL){
            helper(head->next,nodes);
            nodes.push_back(head->val);
        }
        return;
    }
    vector<int> printListFromTailToHead(struct ListNode* head) {
        vector<int> nodes;
        helper(head,nodes);
        return nodes;
    }
};
````


#### 用栈实现代码

````c++
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(struct ListNode* head) {
        stack<int> nodes;
        vector<int> res;
        while(head!=NULL){
            nodes.push(head->val);
            head=head->next;
        }
        int tmp=0;
        while(!nodes.empty()){
            tmp=nodes.top();
            nodes.pop();
            res.push_back(tmp);
        }
        return res;
    }
};
````

### 调试

[从尾到头打印链表](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035)

## 04 重建二叉树

### 题目：

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。

假设输入的前序遍历和中序遍历结果中都不含重复的数字。

例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并输出它的后序遍历序列。

### 思路：

在二叉树的先序遍历序列中，第一个数总是数的根结点的值，后面依次是是左子树结点的值、右子树结点的值；

在二叉树的中序遍历序列中，根节点位于序列中间，根节点左边为左子树，右边为右子树。

根据上述信息，我们可以：

先通过先序遍历序列找到根节点，

然后在中序遍历序列中找到根节点，这样就可以确定左子树和右子树。

接着再回到先序遍历序列中找到左子树和右子树，重复上述步骤（递归）。

### 代码：

````c++
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* reConstructBinaryTree(vector<int> pre,vector<int> vin) {
        return helper(pre,0,pre.size(),vin,0,vin.size());
    }
    
    TreeNode* helper(vector<int>& preorder,int i,int j,vector<int>& inorder,int ii,int jj)
    {

        if(i >= j || ii >= jj)
            return NULL;

        int mid = preorder[i];
        auto f = find(inorder.begin() + ii,inorder.begin() + jj,mid);

        int dis = f - inorder.begin() - ii;

        TreeNode* root = new TreeNode(mid);
        root -> left = helper(preorder,i + 1,i + 1 + dis,inorder,ii,ii + dis);
        root -> right = helper(preorder,i + 1 + dis,j,inorder,ii + dis + 1,jj);
        return root;
    }
};
````

### 调试

[重建二叉树](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6)

## 05 用两个栈实现队列

### 题目

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

### 思路

根据栈的“先进后出”特点，如果将数据导入一个栈，再导入另一个栈，这样数据的出入顺序就变成了“先进先出”，即队列的特点。

假设有两个栈，stack1,stack2.

插入结点：直接压入stack1

删除结点：如果stack2为空，则将stack1中的结点导入stack2,；如果不为空，则从stack2弹出结点。


### 代码

````c++
class Solution
{
public:
    void push(int node) {
        stack1.push(node);
    }
 
    int pop() {
        if(stack2.size()<=0){
            int data;
            while(stack1.size()>0){
                data=stack1.top();
                stack1.pop();
                stack2.push(data);
            }
        }
        if(stack2.size()<=0)
            return -1;
        int del=stack2.top();
        stack2.pop();
        return del;
    }
 
private:
    stack<int> stack1;
    stack<int> stack2;
};
````

### 调试

[用两个栈实现队列](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6)

## 06 旋转数组的最小数字

### 题目：

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。

输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。

例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。

### 思路：

1. 遍历数组，找到数组的最小值，时间复杂度O(n)；
2. 二分查找，时间复杂度O(logn)

    查找过程：

    旋转数组可以看成两个递增（非减）数组，通过前后两个指针left，right分别指向数组的首尾，

    当满足循环不变量时A[left]>=A[right]，mid=(left+right)/2，否则返回A[left]即可;

    如果A[mid]>=A[left]，说明最小值存在mid后面部分，left=mid；

    如果A[mid]<=A[left]，说明最小值存在mid前面部分，right=mid；

    经过循环之后，最终left会指向最小值，返回A[left]即可。

### 代码

````c++
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        int start=0,end=rotateArray.size()-1;
        while (start<end) {
            if (rotateArray[start]<rotateArray[end])
                return rotateArray[start];
            
            int mid = (start+end)/2;
            
            if (rotateArray[mid]>=rotateArray[start]) {
                start = mid+1;
            } else {
                end = mid;
            }
        }
        
        return rotateArray[start];
    }
};
````

### 调试

[旋转数组的最小数字](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba)

## 07 斐波那契数列

### 题目：

现在要求输入一个整数n，请你输出斐波那契数列的第n项。

斐波那契数列的定义：

    f(0)=0;f(1)=1;
    f(n)=f(n-1)+f(n-2)


### 思路：
1. 递归：

    根据递推公式来实现

    优点：代码简单，易懂

    缺点：

    效率低：函数递归调用过程中需要不断分配栈空间，且不断地入栈出栈，代码执行效率低；
    栈溢出：当递归层级太多时，会超出栈容量，导致栈溢出；
    复杂度高：递归调用存在大量的重复计算，时间复杂度以n的指数递增。
2. 循环：

    从前往后计算（动态规划），克服递归出现的缺陷

### 代码

````c++
class Solution {
public:
    int Fibonacci(int n) {
        if(n<2)
            return n;
        int fone=0;
        int ftwo=1;
        int fsum;
        for(int i=2;i<=n;i++){
            fsum=fone+ftwo;
            fone=ftwo;
            ftwo=fsum;
        }
        return fsum;
    }
};
````

### 调试

[斐波那契数列](https://www.nowcoder.com/practice/c6c7742f5ba7442aada113136ddea0c3)

## 08 跳台阶

### 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）.

### 思路

这个其实就是斐波那契数列,对于一个n级的台阶，它要么从它的前一级跳上来，要么从前二级跳上来，所以就有如下等式：


    f(n)=f(n-1)+f(n-2)


至于边界条件的话：


    f(1)=1;f(2)=2


### 代码

````c++
class Solution {
public:
    int jumpFloor(int number) {
        if (number <= 2)
            return number;
        int pre2 = 1, pre1 = 2;
        int result = 1;
        for (int i = 2; i < number; i++) {
            result = pre2 + pre1;
            pre2 = pre1;
            pre1 = result;
        }
        return result;
    }
};
````

### 调试

[跳台阶](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4)

## 09 变态跳台阶

### 题目

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

### 思路

1. 动态规划
    用个数组来保存所有每个台阶的值，然后再从前往后遍历并计算每个台阶的值，每个台阶的值都等于之前台阶的总和
    
    f(n) = f(n-1) + f(n-2) + ... + f(0)

2. 数学推导

    跳上 n-1 级台阶，可以从 n-2 级跳 1 级上去，也可以从 n-3 级跳 2 级上去...，那么

    f(n-1) = f(n-2) + f(n-3) + ... + f(0)

    同样，跳上 n 级台阶，可以从 n-1 级跳 1 级上去，也可以从 n-2 级跳 2 级上去... ，那么

    f(n) = f(n-1) + f(n-2) + ... + f(0)
    
    综上可得

    f(n) - f(n-1) = f(n-1)
    
    即

    f(n) = 2*f(n-1)
    
    所以 f(n) 是一个等比数列


### 代码

#### 动态规划

````c++
class Solution {
public:
    int jumpFloorII(int number) {
        vector<int> dp(number,1);
        for (int i = 1; i < number; i++)
            for (int j = 0; j < i; j++)
                dp[i] += dp[j];
        return dp[number - 1];
    }
};
````

#### 数学推导

````c++
class Solution {
public:
    int jumpFloorII(int number) {
        return pow(2, number - 1);
    }
};
````

### 调试

[变态跳台阶](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387)


## 10 矩形覆盖

### 题目

我们可以用2\*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2\*1的小矩形无重叠地覆盖一个2\*n的大矩形，总共有多少种方法？

### 思路

这个跟跳台阶一个思路

### 代码

代码基本一样

````c++
class Solution {
public:
    int rectCover(int number) {
        if (number <= 2)
            return number;
        int pre2 = 1, pre1 = 2;
        int result = 0;
        for (int i = 3; i <= number; i++) {
            result = pre2 + pre1;
            pre2 = pre1;
            pre1 = result;
        }
        return result;
    }
};
````

### 调试

[矩形覆盖](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6)

## 11 二进制中1的个数

### 题目

输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。

### 思路

1. 首先将整数跟1与，如果结果是1，则累计，然后右移一位，继续前面的步骤，直到这个整数为0
    问题：如果该整数为负数，则会陷入无限循环，为什么？因为负数右移的时候，左边补1，整数右移过程中不可能为0，因此会陷入无限循环。
2. n&(n-1)
    该位运算去除 n 的位级表示中最低的那一位。
    例如下面
    ````
    n       : 10110100
    n-1     : 10110011
    n&(n-1) : 10110000
    ````

### 代码

````c++
class Solution {
public:
     int  NumberOf1(int n) {
         int cnt = 0;
        while (n != 0) {
            cnt++;
            n &= (n - 1);
        }
        return cnt;
     }
};
````

### 调试

[二进制中1的个数](https://www.nowcoder.com/practice/8ee967e43c2c4ec193b040ea7fbb10b8)


## 12 数值的整数次方

### 题目

给定一个 double 类型的浮点数 base 和 int 类型的整数 exponent，求 base 的 exponent 次方。

### 思路

下面的公式中 x 代表 base，n 代表 exponent。

    x^n=n%2?x*(x*x)^(n/2):(x*x)^(n/2)

因为 (x*x)^(n/2) 可以通过递归求解，并且每次递归 n 都减小一半，因此整个算法的时间复杂度为 O(logN)。


### 代码

````c++
class Solution {
public:
    double Power(double base, int exponent) {
        if (exponent == 0)
            return 1;
        if (exponent == 1)
            return base;
        bool isNegative = false;
        if (exponent < 0) {
            exponent = -exponent;
            isNegative = true;
        }
        double pow = Power(base * base, exponent / 2);
        if (exponent % 2 != 0)
            pow = pow * base;
        return isNegative ? 1 / pow : pow;
    }
};
````

### 调试

[数值的整数次方](https://www.nowcoder.com/practice/1a834e5e3e1a4b7ba251417554e07c00)

## 13 调整数组顺序使奇数位于偶数前面

### 题目

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

### 思路

先遍历原数组，累加奇数的个数之后，从原数组里面拷贝一个新数组，然后遍历这个新数组，如果元素是偶数，由于已经算出来奇数的个数了，所以就可以知道偶数要放在原数组的哪个位置了，如果是奇数，就放在原数组开头，然后就是分别累加位置的索引，直到循环结束


### 代码

````c++
class Solution {
public:
    void reOrderArray(vector<int> &array) {
         int oddCnt = 0;
        for (int val : array)
            if (val % 2 == 1)
                oddCnt++;
        vector<int> copy = array;
        int i = 0, j = oddCnt;
        for (int num : copy) {
            if (num % 2 == 1)
                array[i++] = num;
            else
                array[j++] = num;
        }
    }
};
````

### 调试

[调整数组顺序使奇数位于偶数前面](https://www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593)


## 14 链表中倒数第k个结点


### 题目

输入一个链表，输出该链表中倒数第k个结点。

例如：链表中有6个结点，从头到尾依次为1,2,3,4,5,6，则该链表的倒数第3个结点为4.


### 思路

1. 遍历整个链表，计算结点的个数n，再遍历链表，找到第n-k+1个结点；
2. 通过两个指针，第一个指针先走k-1步，到达第k个结点，第二个指针指向头结点，然后两个指针同时走，每次走一步，当第一个指针走到链尾时，第二个指针恰好走到倒数第k个结点。注意细节：链表为空，k大于链表长度或者小于1等情况。


### 代码

````c++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        if(pListHead==NULL || k<=0)
            return NULL;
        ListNode* pAhead=pListHead;
        for(int i=1;i<k;i++){
            if(pAhead->next!=NULL)
                pAhead=pAhead->next;
            else
                return NULL;
        }
        ListNode *pBehind=pListHead;
        while(pAhead->next!=NULL){
            pAhead=pAhead->next;
            pBehind=pBehind->next;
        }
        return pBehind;
    }
};
````

### 调试

[链表中倒数第k个结点](https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a)

## 15 反转链表

### 题目

定义一个函数，输入一个链表的头结点，反转该链表并输出反转后链表的头结点。

### 思路

反转链表，需要调整结点的next指针，例如a->b->c，需要调整为a<-b<-c，只要将当前结点的next指针指向前一结点即可，如b->next=a，需要一个变量来保存前一结点;

但调整当前结点的next指针之后，就无法获取原链表的下一结点了，因此需要一个临时变量来保存当前结点的下一结点。

依次遍历整个链表，调整每个结点的next指针，最后返回原链表的最后一个结点指针即可。

### 代码

````c++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        ListNode* tmp;
        ListNode* pCur=pHead;
        ListNode* pPrev=NULL;
        while(pCur){
            tmp=pCur->next;
            pCur->next=pPrev;
            pPrev=pCur;
            pCur=tmp;
        }
        return pPrev;
    }
};
````

### 调试

[反转链表](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca)

## 16 合并两个排序的链表


### 题目

输入两个递增排序的链表，合并这两个链表并使新链表中的结点仍然时按照递增排序的。

### 思路

合并两个递增排序的链表，思想类似于归并排序的merge过程。

1. 当两个链表均不为空，

    如果链表1头结点的值小于链表2头结点的值，那么链表1的头结点作为新链表的头结点，否则链表2的头结点作为新链表的头结点，链表指针往前走一步；

    对两个链表中剩余结点的操作同步骤1一样；（这是一个递归的过程）

2. 当两个链表至少有一个为空，

    新链表指针指向非空的那一个；

### 代码

#### 递归

````c++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        if(pHead1==NULL)
            return pHead2;
        if(pHead2==NULL)
            return pHead1;
        if(pHead1->val<pHead2->val){
            pHead1->next=Merge(pHead1->next,pHead2);
            return pHead1;
        }
        else{
            pHead2->next=Merge(pHead1,pHead2->next);
            return pHead2;
        }
    }
};
````

#### 迭代

````c++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2)
    {
        ListNode *p=new ListNode(0);
        ListNode *MergeHead=p;
        while(pHead1!=NULL && pHead2!=NULL){
            if(pHead1->val<pHead2->val){
                MergeHead->next=pHead1;
                pHead1=pHead1->next;
            }
            else{
                MergeHead->next=pHead2;
                pHead2=pHead2->next;
            }
            MergeHead=MergeHead->next;
        }
 
        if(pHead1==NULL)
            MergeHead->next=pHead2;
        if(pHead2==NULL)
            MergeHead->next=pHead1;
 
        return p->next;
    }
};
````

### 调试

[合并两个排序的链表](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337)


## 17 树的子结构

### 题目

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

### 思路

判断二叉树B是否为二叉树A的子树：

首先判断二叉树A的根节点值是否等于二叉树B的根节点值；

如果是，则继续往下遍历，判断二叉树A的左子节点和二叉树B的左子结点以及二叉树A的右子节点和二叉树B的右子节点是否都相等，直到叶子节点；（递归）

    return IsSubtree(pRoot1->left,pRoot2->left) && IsSubtree(pRoot1->right,pRoot2->right);

如果不是，则判断二叉树B是否为二叉树A左子树的子树或者二叉树B是否为二叉树A右子树的子树；（递归）

    return HasSubtree(pRoot1->left,pRoot2)|| HasSubtree(pRoot1->right,pRoot2);

### 代码

````c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    bool IsSubtree(TreeNode* pRoot1,TreeNode* pRoot2){
        if(pRoot2==NULL)
            return true;
        if(pRoot1==NULL)
            return false;
        if(pRoot1->val!=pRoot2->val)
            return false;
        return IsSubtree(pRoot1->left,pRoot2->left) && IsSubtree(pRoot1->right,pRoot2->right);
    }
 
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
    {
        bool result=false;
        if(pRoot1!=NULL && pRoot2!=NULL){
            if(pRoot1->val==pRoot2->val)
                result=IsSubtree(pRoot1,pRoot2);
            if(!result)
                return HasSubtree(pRoot1->left,pRoot2)|| HasSubtree(pRoot1->right,pRoot2);
        }
        return result;
    }
};
````

### 调试

[树的子结构](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88)


## 18 二叉树的镜像

### 题目

操作给定的二叉树，将其变换为源二叉树的镜像。

````
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
````

### 思路

观察上面两个二叉树，很容易就可以得出下面求一棵树镜像的过程：

先序遍历这棵树的每个结点，如果遍历到的结点有子结点，则交换它的两个子结点。当交换完所有非叶子结点的左右子结点之后，就得到了树的镜像。


### 代码

````c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    void Mirror(TreeNode *pRoot){
        if(pRoot==NULL)
            return;
        if(pRoot->left==NULL && pRoot->right==NULL)
            return;
        TreeNode* tmp=pRoot->left;
        pRoot->left=pRoot->right;
        pRoot->right=tmp;
         
        if(pRoot->left)
            Mirror(pRoot->left);
        if(pRoot->right)
            Mirror(pRoot->right);
    }
};
````

### 调试

[二叉树的镜像](https://www.nowcoder.com/practice/564f4c26aa584921bc75623e48ca3011)

## 19 顺时针打印矩阵

### 题目

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

### 思路

其实就是绕着这个矩阵的边绕圈，遇到“墙”就转弯(顺时针),一圈过后，缩小范围，继续循环直到圈汇聚到一点。

### 代码

````c++
class Solution {
public:
    vector<int> printMatrix(vector<vector<int> > matrix) {
        vector<int> ret;
        int r1 = 0, r2 = matrix.size() - 1, c1 = 0, c2 = matrix[0].size() - 1;
        while (r1 <= r2 && c1 <= c2) {
            for (int i = c1; i <= c2; i++)
                ret.push_back(matrix[r1][i]);
            for (int i = r1 + 1; i <= r2; i++)
                ret.push_back(matrix[i][c2]);
            if (r1 != r2)
                for (int i = c2 - 1; i >= c1; i--)
                    ret.push_back(matrix[r2][i]);
            if (c1 != c2)
                for (int i = r2 - 1; i > r1; i--)
                    ret.push_back(matrix[i][c1]);
            r1++; r2--; c1++; c2--;
        }
        return ret;
    }
};
````

### 调试

[顺时针打印矩阵](https://www.nowcoder.com/practice/9b4c81a02cd34f76be2659fa0d54342a)


## 20 包含min函数的栈

### 题目

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

### 思路

在内部定义两个栈，第一个栈用来存储进来的值，第二个栈用来存最小值，下面代码就是很好的解释

### 代码

````c++
class Solution {
private:
    stack<int> s1;
    stack<int> s2;
public:
    void push(int value) {
        s1.push(value);
	    if (s2.empty() || value <= min())  s2.push(value);
    }
    void pop() {
         if (s1.top() == min())  s2.pop();
	        s1.pop();
    }
    int top() {
        return s1.top();
    }
    int min() {
        return s2.top();
    }
};
````

### 调试

[包含min函数的栈](https://www.nowcoder.com/practice/4c776177d2c04c2494f2555c9fcc1e49)

## 21 栈的压入、弹出序列

### 题目

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

### 思路

借用一个额外的辅助栈

举例：

入栈1,2,3,4,5

出栈4,5,3,2,1

遍历压栈顺序，先将第一个放入栈中，这里是1，然后判断栈顶元素是不是出栈顺序的第一个元素，这里是4，很显然1≠4，所以我们继续压栈，直到相等以后开始出栈，出栈一个元素，则将出栈顺序向后移动一位，直到不相等，这样循环等压栈顺序遍历完成，如果辅助栈还不为空，说明弹出序列不是该栈的弹出顺序。

首先1入辅助栈，此时栈顶1≠4，继续入栈2

此时栈顶2≠4，继续入栈3

此时栈顶3≠4，继续入栈4

此时栈顶4＝4，出栈4，弹出序列的位置向后移一位，此时为5，,辅助栈里面是1,2,3

此时栈顶3≠5，继续入栈5

此时栈顶5=5，出栈5,弹出序列向后一位，此时为3，,辅助栈里面是1,2,3

….

依次执行，最后辅助栈为空。如果不为空说明弹出序列不是该栈的弹出顺序

### 代码

````c++
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
      if(pushV.size()==0||popV.size()==0||popV.size()!=pushV.size())
          return false;
      stack<int> stack;
      int j=0;
      for(int i=0;i<pushV.size();i++){
          stack.push(pushV[i]);
          while(!stack.empty()&&stack.top()==popV[j]){
               stack.pop();
               j++;
           }
       }
       return stack.empty();
    }
};
````

### 调试

[栈的压入、弹出序列](https://www.nowcoder.com/practice/d77d11405cc7470d82554cb392585106)

## 22 从上往下打印二叉树

### 题目

从上往下打印出二叉树的每个节点，同层节点从左至右打印

### 思路

二叉树的层序遍历，标准bfs（广度优先搜索），从根结点开始放入一个队列，一边把子节点放入队，一边出队，直到队列为空。出队的过程就是一个层序遍历。

### 代码

````c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    vector<int> PrintFromTopToBottom(TreeNode* root) {
       vector<int> res;
       queue<TreeNode*> q;
        if(root==NULL)return res;
        q.push(root);
        while(!q.empty()){
            TreeNode* tmp=q.front();
            q.pop();
            if(tmp->left!=NULL) q.push(tmp->left);
            if(tmp->right!=NULL) q.push(tmp->right);
            res.push_back(tmp->val);
        }   
        return res;
    }
};
````

### 调试

[从上往下打印二叉树](https://www.nowcoder.com/practice/7fe2212963db4790b57431d9ed259701)


## 23 二叉搜索树的后序遍历序列

### 题目

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。

### 思路

二叉搜索树首先是有序的，其后序遍历是“左右根”的顺序，根节点总是在后面，剩余部分分成两部分，比根小的是左子树，比根大的是右子树。（递归）

举例：

* 判断序列{5,7,6,9,11,10,8}是否是二叉排序树的后序遍历。其中，8是根节点，{5,7,6}比8小是左子树，{9,11,10}比8大是右子树。
* 判断{5,7,6}是否是二叉排序树，其中6是根节点，5比6小是左子树，7比6大是右子树。
* 判断{9,11,10}是否是二叉排序树，其中10是根节点，9比10小是左子树，11比10大是右子树。

### 代码

````c++
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        return helper(sequence, 0, sequence.size() - 1);
    }

    bool helper(vector<int> seq, int begin, int end){
        if(seq.empty() || begin > end)
            return false;
 
        int i = begin;
        for(; i < end; ++i)
            if(seq[i] > seq[end])
                break;
 
        int j = i;
        for(; j < end; ++j)
            if(seq[j] < seq[end])
                return false;
 
        bool left = true;
        if(i > begin)
            left = helper(seq, begin, i - 1);
 
        bool right = true;
        if(i < end - 1)
            right = helper(seq, i , end - 1);
 
        return left && right;
    }
};
````

### 调试

[二叉搜索树的后序遍历序列](https://www.nowcoder.com/practice/a861533d45854474ac791d90e447bafd)


## 24 二叉树中和为某一值的路径

### 题目

输入一颗二叉树的跟节点和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。(注意: 在返回值的list中，数组长度大的数组靠前)

### 思路

回溯算法的典型案例，也是深度优先搜素(dfs)的典型案例

如果当前结点不为空，且结点的值小于期望值，则将该结点压入路径vector中，并继续从左右子结点往下遍历；

    if(root->left)   FindPath(root->left,result,path,expectedNumber-root->val);
    if(root->right)  FindPath(root->right,result,path,expectedNumber-root->val);

递归的结束条件：

当遍历到了叶子节点，且该叶子结点的值等于期望值，那么这是一条满足的路径；

每次检查完一条路径后，要弹出路径的一个节点，选择另外个节点压入，继续递归下去

### 代码

````c++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    vector<vector<int> > FindPath(TreeNode* root,int expectNumber) {
        vector<vector<int> > res;
        if(root==NULL)
            return res;
        vector<int> path;
        FindPath(root,res,path,expectNumber);
        return res;
    }
     
    void FindPath(TreeNode* root,vector<vector<int> > &result,vector<int> &path,int expectedNumber){
        if(root->val>expectedNumber)
            return;
        path.push_back(root->val);
        if(root->left==NULL && root->right==NULL && root->val==expectedNumber){
            result.push_back(path);
        }
        if(root->left)
            FindPath(root->left,result,path,expectedNumber-root->val);
        if(root->right)
            FindPath(root->right,result,path,expectedNumber-root->val);
        path.pop_back();
    }
};
````

### 调试

[二叉树中和为某一值的路径](https://www.nowcoder.com/practice/b736e784e3e34731af99065031301bca)