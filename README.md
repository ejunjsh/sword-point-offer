# sword-point-offer

剑指offer 解题集，顺便学c++

题目都来自于牛客网的[剑指offer](https://www.nowcoder.com/ta/coding-interviews)题集，可以拷贝代码到相关题目上调试

## 01 [二维数组中的查找](https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e)

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

## 02 [替换空格](https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423)

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

## 03 [从尾到头打印链表](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035)

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

## 04 [重建二叉树](https://www.nowcoder.com/practice/8a19cbe657394eeaac2f6ea9b0f6fcf6)

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

## 05 [用两个栈实现队列](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6)

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

## 06 [旋转数组的最小数字](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba)

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

## 07 [斐波那契数列](https://www.nowcoder.com/practice/c6c7742f5ba7442aada113136ddea0c3)

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

## 08 [跳台阶](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4)

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


## 09 [变态跳台阶](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387)

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

## 10 [矩形覆盖](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6)

### 题目

我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

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
