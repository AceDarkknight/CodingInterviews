# CodingInterviews
网上大部分《剑指offer》的实现都是基于 Java、python或者c++的，笔者也试着用 C# 实现一下。所有代码均通过牛客测试。

## 斐波那契数列
#### 题目描述
大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项。n<=39

[牛客](https://www.nowcoder.com/practice/c6c7742f5ba7442aada113136ddea0c3?tpId=13&tqId=11160&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public int Fibonacci(int n)
{
    // write code here
        if (n <= 0)
        {
            return 0;
        }
    
        int[] r = new int[n];
        for (int i = 0; i < n; i++)
        {
            if (i == 0 || i == 1)
            {
                r[i] = 1;
            }
            else
            {
                r[i] = r[i - 1] + r[i - 2];
            }
        }
        return r[n - 1];
}
```
## 跳台阶
#### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

[牛客](https://www.nowcoder.com/practice/8c82a5b80378478f9484d87d1c5f12a4?tpId=13&tqId=11161&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)
```cs
public int jumpFloor(int number)
{
    if (number <= 0)
    {
        return 0;
    }

    if (number == 1 || number == 2)
    {
        return number;
    }

    return jumpFloor(number - 1) + jumpFloor(number - 2);
}
```
## 变态跳台阶
#### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

[牛客](https://www.nowcoder.com/practice/22243d016f6b47f2a6928b4313c85387?tpId=13&tqId=11162&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public int jumpFloorII(int number)
{
    if (number <= 2)
    {
        return number;
    }

    int[] r = new int[number+1];
    int t = 0;
    for (int i = 0; i <= number; i++)
    {
        if (i < 3)
        {
            r[i] = i;
        }
        else
        {
            r[i] = t + 1;
        }

        t += r[i];
    }

    return r[number];
}
```
递归实现
```cs
public int jumpFloorIIV2(int number)
{
    if (number <= 0)
    {
        return 0;
    }

    if (number == 1)
    {
        return number;
    }

    return 2 * jumpFloorIIV2(number - 1);
}
```
## 矩形覆盖
#### 题目描述

我们可以用2\*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2\*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

[牛客](https://www.nowcoder.com/practice/72a5a919508a4251859fb2cfb987a0e6?tpId=13&tqId=11163&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public int rectCover(int number)
{
    if (number <= 0)
    {
        return 0;
    }

    if (number <= 2)
    {
        return number;
    }

    return rectCover(number - 1) + rectCover(number - 2);
}
```
## 调整数组顺序使奇数位于偶数前面
#### 题目描述
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

[牛客](https://www.nowcoder.com/practice/beb5aa231adc45b2a5dcc5b62c93f593?tpId=13&tqId=11166&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public int[] reOrderArray(int[] array)
{
    if (array ==null || array.Length <= 1)
    {
        return array;
    }

    List<int> evenList = new List<int>();
    List<int> oddList = new List<int>();
    foreach(int i in array)
    {
        if (i % 2 == 0)
        {
            evenList.Add(i);
        }
        else
        {
            oddList.Add(i);
        }
    }

    oddList.AddRange(evenList);
    return oddList.ToArray();
}
```
## 从尾到头打印链表
输入一个链表，从尾到头打印链表每个节点的值。  
[牛客](https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tqId=11156&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
// 返回从尾到头的列表值序列
public List<int> printListFromTailToHead(ListNode listNode)
{
    Stack<int> result = new Stack<int>();

    ListNode currentNode = listNode;
    while (currentNode != null)
    {
        result.Push(currentNode.val);
        currentNode = currentNode.next;
    }

    return result.ToList();
}
```
递归实现
```cs
// 返回从尾到头的列表值序列
List<int> list1 = new List<int>();
public List<int> printListFromTailToHeadV2(ListNode listNode)
{
    if (listNode != null)
    {
        printListFromTailToHeadV2(listNode.next);
        list1.Add(listNode.val);
    }

    return list1;
}
```
## 用两个栈实现队列
用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。  
[牛客](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=11158&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
Stack<int> inStack = new Stack<int>();
Stack<int> outStack = new Stack<int>();
public void push(int node)
{
    this.inStack.Push(node);
}

public int pop()
{
    if (this.outStack.Count != 0)
    {
        return this.outStack.Pop();
    }

    // inStack pop 后，长度发生变化，直接使用 i<inStack.Count 会得到错误结果，需要使用 length 代表初始长度。
    int length = this.inStack.Count;
    for (int i = 0; i < length; i++)
    {
        this.outStack.Push(this.inStack.Pop());
    }

    return this.outStack.Pop();
}
```
