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

## 3 [从尾到头打印链表](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035)

### 题目：

输入一个链表的头结点，从尾到头反过来打印每个结点的值。

### 思路：

1. 改变链表结构的话，先反转链表，然后从头到尾打印每个结点的值。
2. 无需改变链表结构，使用栈，遍历整个链表，将结点依次入栈，然后再依次出栈，实现“后进先出”。
3. 无需改变链表结构，递归实现,如果链表结点数过多的话，可能会导致栈溢出。

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