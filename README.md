# sword-point-offer

《剑指offer》解题集，顺便学c++

题目都来自于牛客网的[剑指offer](https://www.nowcoder.com/ta/coding-interviews)题集，可以拷贝代码到相应题目上调试

## 01 二维数组中的查找

### 描述：

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

### 描述：

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

### 描述：

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

### 描述：

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

### 描述

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

### 描述：

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

### 描述：

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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


### 描述

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

### 描述

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


### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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

### 描述

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


## 25 复杂链表的复制

### 描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的head。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

### 思路

1. 在原链表的每个节点后面拷贝出一个新的节点
2. 依次给新的节点的随机指针赋值，而且这个赋值非常容易 cur->next->random = cur->random->next
3. 断开原链表和拷贝链表的链接，即得到深度拷贝后的新链表

下面图会比较清晰点

[![](https://raw.githubusercontent.com/ejunjsh/sword-point-offer/master/images/randomlist.png)](https://raw.githubusercontent.com/ejunjsh/sword-point-offer/master/images/randomlist.png)

### 代码

````c++
/*
struct RandomListNode {
    int label;
    struct RandomListNode *next, *random;
    RandomListNode(int x) :
            label(x), next(NULL), random(NULL) {
    }
};
*/
class Solution {
public:
    RandomListNode* Clone(RandomListNode* head)
    {
        RandomListNode * head_cp = nullptr, * cur = head, * cur_cp = nullptr;
        if (head == nullptr)
            return nullptr;
        //在原链表的每个节点后面拷贝出一个新的节点
        while (cur != nullptr)
        {
            cur_cp = new RandomListNode(cur->label);
            cur_cp->next = cur->next;
            cur->next = cur_cp;
            cur = cur_cp->next;
        }
        cur = head;
        //依次给新的节点的随机指针赋值，而且这个赋值非常容易 cur->next->random = cur->random->next
        while (cur != nullptr)
        {
            cur_cp = cur->next;
            if (cur->random)
                cur_cp->random = cur->random->next;
            cur = cur_cp ->next;
        }
        cur = head;
        head_cp = head->next;
        //断开原链表和拷贝链表的链接，即得到深度拷贝后的新链表
        while (cur != nullptr)
        {
            cur_cp = cur->next;
            cur->next = cur_cp->next;
            cur = cur->next;
            if (cur)
                cur_cp->next = cur->next;
        }
        return head_cp;
    }
};
````

### 调试

[复杂链表的复制](https://www.nowcoder.com/practice/f836b2c43afc4b35ad6adc41ec941dba)


## 26 二叉搜索树与双向链表

### 描述

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

### 思路

要得出一个排序的链表，所以必须要`中序遍历`，并在遍历中处理双向的链接。

首先定义个`head`字段用来记录头节点，一旦找到第一个节点，就赋值给`head`

然后定义`pre`字段用来记录遍历中之前加入链表的节点，一旦确认一个节点加入到列表，就要用`pre`作为这个节点的左节点`node->left = pre`，把这个节点作为`pre`的右节点`pre->right = node`,之后当前节点赋值给`pre`，继续遍历。

详细看代码吧

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
    TreeNode* Convert(TreeNode* pRootOfTree)
    {
        helper(pRootOfTree);
        return head;
    }
private:
    TreeNode* head=NULL;
    TreeNode* pre=NULL;

    void helper(TreeNode* node){
        if (node == NULL)
            return;
        // 中序遍历标准递归
        helper(node->left);
        //node的左边放pre
        node->left = pre;
        if (pre != NULL)
             //pre的右边放node
            pre->right = node;
        //把node赋值给pre
        pre = node;
        if (head == NULL)
            //找到头节点了
            head = node;
        //中序遍历标准递归
        helper(node->right);
    }
};
````

### 调试

[二叉搜索树与双向链表](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5)

## 27 字符串的排列

### 描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

__输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。__

### 思路

标准的回溯算法题

把一个字符串看成两部分组成：第一部分为第一个字符，第二部分为后面的所有字符。

求整个字符串的排列，可以看出两步：首先求所有可能出现在第一个位置的字符，即把第一个字符和后面的所有字符交换；然后固定第一个字符，求后面所有字符的排序。此时仍把后面的字符看成两部分，第一个字符和后面的字符，然后重复上述步骤。（递归）


### 代码
````c++
class Solution {
public:
    void swap(char* c1,char* c2){
        char tmp=*c1;
        *c1=*c2;
        *c2=tmp;
    }
     
    void Permutation(string &str,int begin,vector<string> &result){
        int len=str.length();
        if(begin==len-1)
            result.push_back(str);
        else{
            for(int i=begin;i<len;i++){
                if(i==begin || str[i]!=str[begin]){
                    swap(&str[begin],&str[i]);
                    Permutation(str,begin+1,result);
                    swap(&str[begin],&str[i]);  
                }
            }
        }
    }
     
    vector<string> Permutation(string str) {
        vector<string> result;
        if(str.length()>0){
            Permutation(str,0,result);
            sort(result.begin(),result.end());
        }
        return result;
    }
};
````

### 调试

[字符串的排列](https://www.nowcoder.com/practice/fe6b651b66ae47d7acce78ffdd9a96c7)

## 28 数组中出现次数超过一半的数字

### 描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

### 思路

多数投票问题，可以利用 Boyer-Moore Majority Vote Algorithm 来解决这个问题，使得时间复杂度为 O(N)。

这个算法也很好理解，就是投票。遍历数组，用`major`, `counts`分别记录大多数的值和它相应的票数。如果遇到反对的（遍历的时候发现跟`major`不同的），就减一，赞同的就加一。如果票数变为零，而且跟`major`不同，`major`就换个数字，直到遍历结束。这时候`major`的值就是就是答案了，但是这个题是可以存在没有超过一半的数字的情况的，所以，接下来还要验证这个`major`是不是大多数，再来一次遍历，确认`major`是否超过数组一半，如果，没超过那就不存在大多数的数了，所以返回0，如果超过，那`major`就是答案了。


### 代码

````c++
class Solution {
public:
    int MoreThanHalfNum_Solution(vector<int> numbers) {
        int major, counts = 0, n = numbers.size();
        for (int i = 0; i < n; i++) {
            if (!counts) {
                major = numbers[i];
                counts = 1;
            }
            else counts += (numbers[i] == major) ? 1 : -1;
        }
        
        int cnt = 0;
        for (auto val : numbers)
            if (val == major)
                cnt++;
        return cnt > numbers.size() / 2 ? major : 0;
    }
};
````

### 调试

[数组中出现次数超过一半的数字](https://www.nowcoder.com/practice/e8a1b01a2df14cb2b228b30ee6a92163)

## 29 最小的K个数

### 描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

### 思路

有两个方案：

1. 快排
    快速排序的 partition() 方法，会返回一个整数 j 使得 a[l..j-1] 小于等于 a[j]，且 a[j+1..h] 大于等于 a[j]，此时 a[j] 就是数组的第 j 大元素。可以利用这个特性找出数组的第 K 个元素，这种找第 K 个元素的算法称为快速选择算法。
2. 最大堆
    构建k个整数的最大堆数据结构，然后将剩余n-k个整数依次与堆顶比较，大则抛弃，小则删除堆顶并插入，最后的最大堆就是最小的k个整数.

### 代码

#### 快排

````c++
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> ret;
        if (k > input.size() || k <= 0)
            return ret;
        findKthSmallest(input, k - 1);
        for (int i = 0; i < k; i++)
            ret.push_back(input[i]);
        return ret;
    }
    
private:
    void findKthSmallest(vector<int>& nums, int k) {
        int l = 0, h = nums.size() - 1;
        while (l < h) {
            int j = partition(nums, l, h);
            if (j == k)
                break;
            if (j > k)
                h = j - 1;
            else
                l = j + 1;
        }
    }

    int partition(vector<int>& nums, int l, int h) {
        int p = nums[l];
        int i = l, j = h + 1;
        while (true) {
            while (i != h && nums[++i] < p) ;
            while (j != l && nums[--j] > p) ;
            if (i >= j)
                break;
            swap(nums[i],nums[j]);
        }
        swap(nums[l],nums[j]);
        return j;
    }
};
````

#### 最大堆

````c++
class Solution {
public:
    typedef priority_queue<int,vector<int>,less<int> > PQ;
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int> output;
        if(k<1 || input.size()<k)
            return output;
 
        PQ LeastNumbers;
        for(auto it=input.begin();it!=input.end();it++){
            if(LeastNumbers.size()<k)
                LeastNumbers.push(*it);
            else{
                int greatest=LeastNumbers.top();
                if(*it<greatest){
                    LeastNumbers.pop();
                    LeastNumbers.push(*it);
                }
            }
        }
        while(!LeastNumbers.empty()){
            output.push_back(LeastNumbers.top());
            LeastNumbers.pop();
        }
 
        return output;
    }
};
````

### 调试

[最小的K个数](https://www.nowcoder.com/practice/6a296eb82cf844ca8539b57c23e6e9bf)

## 30 连续子数组的最大和

### 描述

HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1)

### 思路

典型的动态规划

假设f(i)为以第i个数字结尾的子数组的最大和，那么

    if f(i-1)<=0 f(i)=A[i]
    if f(i-1)>0  f(i)=f(i-1)+A[i]

初始状态：f(0)=A[0]

max（f(0)...f(i)）就是答案

这里可以优化一下，就是用一个变量`sum`表示f(i-1),因为整个循环下来就只需要f(i-1)的值，其余的值都不需要保存。

### 代码

````c++
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
           if (array.size() == 0)
                return 0;
            int greatestSum = INT_MIN;
            int sum = 0;
            for (int val : array) {
                sum = sum <= 0 ? val : sum + val;
                greatestSum = max(greatestSum, sum);
            }
            return greatestSum;
    }
};
````

### 调试

[连续子数组的最大和](https://www.nowcoder.com/practice/459bd355da1549fa8a49e350bf3df484)


## 31 整数中1出现的次数（从1到n整数中1出现的次数）

### 描述

求出1~13的整数中1出现的次数,并算出100~1300的整数中1出现的次数？为此他特别数了一下1~13中包含1的数字有1、10、11、12、13因此共出现6次,但是对于后面问题他就没辙了。ACMer希望你们帮帮他,并把问题更加普遍化,可以很快的求出任意非负整数区间中1出现的次数（从1 到 n 中1出现的次数）。

### 思路


累加1到n中每个整数1出现的次数。

求每个整数1出现的个数：通过对10求余数，判断整数的个位是否为1，如果商不为0，则继续除以10再判断个位数字是否为1.

### 代码

````c++
class Solution {
public:
    int NumberOf1Between1AndN_Solution(int n)
    {
        int count=0;
        for(int i=1;i<=n;i++)
            count+=numberOf1(i);
        return count;
    }
     
    int numberOf1(int n){
        int count=0;
        while(n){
            if(n%10==1)
                count++;
            n=n/10;
        }
        return count;
    }
};
````

### 调试

[整数中1出现的次数（从1到n整数中1出现的次数）](https://www.nowcoder.com/practice/bd7f978302044eee894445e244c7eee6)

## 32 把数组排成最小的数

### 描述

输入一个正整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。例如输入数组{3，32，321}，则打印出这三个数字能排成的最小数字为321323。

### 思路

这道题其实就是对数组排序，哪个在前哪个在后，只要给出一个合适的比较方法即可。

    if mn>nm n要在m之前
    if mn<nm m要在n之前

    其中n，m分别是数组的元素，mn代表这个两个元素的字符串拼接后的字符串，mn和nm这两个字符串的比较的结果基本可以决定排序的结果了。

例如 3 32两个元素，"332">"323" ,所以32要排在3之前

### 代码

````c++
class Solution {
public:
    static bool compare(int a,int b){
        string strNum1=to_string(a);
        string strNum2=to_string(b);
        return (strNum1+strNum2)<(strNum2+strNum1);
    }
     
    string PrintMinNumber(vector<int> numbers) {
        string result;
        if(numbers.empty())
            return result;
        sort(numbers.begin(),numbers.end(),compare);
        for(auto i=0;i<numbers.size();i++)
            result+=to_string(numbers[i]);
        return result;
    }
};
````

### 调试

[把数组排成最小的数](https://www.nowcoder.com/practice/8fecd3f8ba334add803bf2a06af1b993)


## 33 丑数

### 描述

把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。

### 思路

还是动态规划吧

用一个N大小的数组记录从小到大的丑数，通过之前数组里面的丑数可以算出接下来的丑数,下面代码就是自解释的代码

### 代码

````c++
class Solution {
public:
    int GetUglyNumber_Solution(int index) {
         if (index <= 6)
            return index;
        int i2 = 0, i3 = 0, i5 = 0;
        vector<int> dp(index,0);
        dp[0] = 1;
        for (int i = 1; i < index; i++) {
            int next2 = dp[i2] * 2, next3 = dp[i3] * 3, next5 = dp[i5] * 5;
            dp[i] = min(next2, min(next3, next5));
            if (dp[i] == next2)
                i2++;
            if (dp[i] == next3)
                i3++;
            if (dp[i] == next5)
                i5++;
        }
        return dp[index - 1];
    }
};
````

### 调试

[丑数](https://www.nowcoder.com/practice/6aa9e04fc3794f68acf8778237ba065b)

## 34 第一个只出现一次的字符

### 描述

在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.

### 思路

基本思路可以用hashmap，key是字符，value是出现的次数，遍历两次，第一次填充hashmap，第二次就取出次数为一的字符。

但是如果确认是ASCII字符的话，就建一个256的数组，索引为字符的ASCII码，值是次数，接下来跟上面一样了，代码用的是数组方式。

### 代码

````c++
class Solution {
public:
    int FirstNotRepeatingChar(string str) {
        vector<int> cnts(256,0);
        for (int i = 0; i < str.size(); i++)
            cnts[str[i]]++;
        for (int i = 0; i < str.size(); i++)
            if (cnts[str[i]] == 1)
                return i;
        return -1;
    }
};
````

### 调试

[第一个只出现一次的字符](https://www.nowcoder.com/practice/1c82e8cf713b4bbeb2a5b31cf5b0417c)

## 35 数组中的逆序对

### 描述

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组,求出这个数组中的逆序对的总数P。并将P对1000000007取模的结果输出。 即输出P%1000000007

### 思路

最简单的方法就是遍历每个元素，对于每个元素跟它前面后面的每个元素比较，如果比前面小，就加一，比后面大就加一

还有一个方法就是归并，把数组进行二分(divide)，不断递归下去,然后当分到只有两个元素时候，开始合并(merge)，合并就为了排序和累计逆序对的数量，每次合并之后都是一个升序排序的数组。

合并就做了两件事
1. 在数组里面选择头元素和中间的那个元素比较，如果前面大话，就把他们的索引之差加到累计的变量里面，为什么呢，因为前面到中间的那段数组已经是有序的了，所以头元素大的话，那么在他们之间的元素都大于中间那个。之后小的那个元素放入临时数组。然后再选择两个元素，重复上面。
2. 把临时数组的值拷进原来的数组


例如：

    4 3 2 1

    divide : 4 3 | 2 1  
    merge: 4 3  
        4比3大，所以cnt+1
    merge: 2 1  
        2比1大，所以cnt+1
    merge： 3 4 1 2  
        1 比 4 和 3 都小，所以cnt+2
        2 比 4 和 3 都小，所以cnt+2

所以cnt=6

### 代码

````c++
class Solution {
public:
    int InversePairs(vector<int> data) {
        tmp = vector<int>(data.size());
        divide(data, 0, data.size() - 1);
        return (int) (cnt % 1000000007);
    }
    
private:
    long cnt = 0;
    vector<int> tmp; 

    void divide(vector<int>& nums, int l, int h) {
        if (h - l < 1)
            return;
        int m = l + (h - l) / 2;
        divide(nums, l, m);
        divide(nums, m + 1, h);
        merge(nums, l, m, h);
    }

    void merge(vector<int>& nums, int l, int m, int h) {
        int i = l, j = m + 1, k = l;
        while (i <= m || j <= h) {
            if (i > m)
                tmp[k] = nums[j++];
            else if (j > h)
                tmp[k] = nums[i++];
            else if (nums[i] < nums[j])
                tmp[k] = nums[i++];
            else {
                tmp[k] = nums[j++];
                cnt += m - i + 1; 
            }
            k++;
        }
        for (k = l; k <= h; k++)
            nums[k] = tmp[k];
    }
};
````

### 调试

[数组中的逆序对](https://www.nowcoder.com/practice/96bd6684e04a44eb80e6a68efc0ec6c5)

## 36 两个链表的第一个公共结点

### 描述

输入两个链表，找出它们的第一个公共结点。

### 思路

你可以比喻两个人分别从他们家出门，去上学，总有一天会在上学路上碰上面的。所以只要走到链表结尾（学校），就立即又从链表头开始（家），肯定会相遇的。

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
    ListNode* FindFirstCommonNode( ListNode* pHead1, ListNode* pHead2) {
        ListNode* l1 = pHead1;
        ListNode* l2 = pHead2;
        while (l1 != l2) {
            l1 = (l1 == NULL) ? pHead1 : l1->next;
            l2 = (l2 == NULL) ? pHead2 : l2->next;
        }
        return l1;
    }
};
````

### 调试

[两个链表的第一个公共结点](https://www.nowcoder.com/practice/6ab1d9a29e88450685099d45c9e31e46)


## 37 数字在排序数组中出现的次数

### 描述

统计一个数字在排序数组中出现的次数。

### 思路

二分查找，查找这个数字第一次出现的位置，和最后一次出现的位置，相减就是答案了。

### 代码

````c++
class Solution {
public:
    int GetNumberOfK(vector<int> data ,int k) {
        int first = binarySearch(data, k);
        int last = binarySearch(data, k + 1); //搜索比这个数字大1的数字，即搜索这个数字最后一次出现的位置
        return (first == data.size() || data[first] != k) ? 0 : last - first;
    }
    
private:
    int binarySearch(vector<int>& nums, int k) {
        int l = 0, h = nums.size();
        while (l < h) {
            int m = l + (h - l) / 2;
            if (nums[m] >= k)
                h = m;
            else
                l = m + 1;
        }
        return l;
    }
};
````

### 调试

[数字在排序数组中出现的次数](https://www.nowcoder.com/practice/70610bf967994b22bb1c26f9ae901fa2)

## 38 二叉树的深度

### 描述

输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。

### 思路

dfs递归，下面代码一看就明白的了

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
    int TreeDepth(TreeNode* pRoot)
    {
        return pRoot == NULL ? 0 : 1 + max(TreeDepth(pRoot->left), TreeDepth(pRoot->right));
    }
};
````

### 调试

[二叉树的深度](https://www.nowcoder.com/practice/435fb86331474282a3499955f0a41e8b)


## 39 平衡二叉树

### 描述

输入一棵二叉树，判断该二叉树是否是平衡二叉树。平衡二叉树左右子树高度差不超过 1。

### 思路

还是dfs递归下去，下面代码一看就明白的了

### 代码

````c++
class Solution {
private:
    bool isBalanced=true;
    int height(TreeNode* root) {
        if (root == NULL || !isBalanced)
            return 0;
        int left = height(root->left);
        int right = height(root->right);
        if (abs(left - right) > 1)
            isBalanced = false;
        return 1 + max(left, right);
    }
public:
    bool IsBalanced_Solution(TreeNode* pRoot) {
        height(pRoot);
        return isBalanced;
    }
};
````

### 调试

[平衡二叉树](https://www.nowcoder.com/practice/8b3b95850edb4115918ecebdf1b4d222)

## 40 数组中只出现一次的数字

### 描述

一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。

### 思路

因为

    a ^ a=0;
    0 ^ b=b;
所以
 
    a ^ b ^ a = b

b在[a,b,a]是出现一次的数字

可现在有两个出现一次的数字了，例如 [a,b,a,c],那么对它们每个异或一次的结果是

    diff=a ^ b ^ a ^ c = b ^ c

这还是解不出来啊，别急，如果将上面的数组分成两个，每个分别有一个出现一次的数字，

那么就可以对每个数组的每个元素异或，就可以找出那两个数字了.

如何分数组呢？

上面的diff的用处就是他的最右为1的位，可以用这个条件来分数组。因为异或为1的位，代表了两个数字在这个位不同。

所以 b 和 c在那个位肯定是0和1或者1和0。利用这点就可以分数组了。

理解上面的话，代码就不难理解了。

### 代码

````c++
class Solution {
public:
    void FindNumsAppearOnce(vector<int> data,int* num1,int *num2) {
       int diff = 0;
        for (int num : data)
            diff ^= num;
        diff &= -diff; //求出最右为1的位，其余为零
        for (int num : data) {
            if ((num & diff) == 0)  
                *num1 ^= num; // 位为0
            else
                *num2 ^= num; // 位为1
        }
    }
};
````

### 调试

[数组中只出现一次的数字](https://www.nowcoder.com/practice/e02fdb54d7524710a7d664d082bb7811)

## 41 和为S的连续正数序列

### 描述

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

> 输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

### 思路

由于数字是连续的，所以这条题其实就是要你找出开始的位置和结束的位置即可。

使用双指针，一个记录头，一个记录尾，按照条件，把头或尾累加或剔除，满足条件的加入到结果集里面

下面代码就很好理解了

### 代码

````c++
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
        vector<vector<int> > ret;
        int start = 1, end = 2;
        int curSum = 3;
        while (end < sum) {
            if (curSum > sum) {
                curSum -= start;
                start++;
            } else if (curSum < sum) {
                end++;
                curSum += end;
            } else {
                vector<int> list;
                for (int i = start; i <= end; i++)
                    list.push_back(i);
                ret.push_back(list);
                curSum -= start;
                start++;
                end++;
                curSum += end;
            }
        }
        return ret;
    }
};
````

### 调试

[和为S的连续正数序列](https://www.nowcoder.com/practice/c451a3fd84b64cb19485dad758a55ebe)

## 42 和为S的两个数字

### 描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

### 思路

这道题跟上一道一样，也是双指针，但是更简单

下面代码算是可以自解释的了

### 代码

````c++
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        int i = 0, j = array.size() - 1;
        while (i < j) {
            int cur = array[i] + array[j];
            if (cur == sum)
                return {array[i],array[j]};
            if (cur < sum)
                i++; 
            else
                j--;
        }
        return vector<int>();
    }
};
````

### 调试

[和为S的两个数字](https://www.nowcoder.com/practice/390da4f7a00f44bea7c2f3d19491311b)

## 43 左旋转字符串

### 描述

汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！

### 思路

先反转前面k个字符，再反转剩下的字符，最后对整个字符串再反转。

### 代码

````c++
class Solution {
public:
    string LeftRotateString(string str, int n) {
      if (n >= str.size())
        return str;
      reverse(str.begin(),str.begin()+n);
      reverse(str.begin()+n, str.end());
      reverse(str.begin(),str.end());
      return str;    
    }
};
````

### 调试

[左旋转字符串](https://www.nowcoder.com/practice/12d959b108cb42b1ab72cef4d36af5ec)