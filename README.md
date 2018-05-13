网上大部分《剑指offer》的实现都是基于 Java、python或者c++的，笔者也试着用 C# 实现一下。所有代码均通过牛客网测试。

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
public int jumpFloorII(int number)
{
    if (number <= 0)
    {
        return 0;
    }

    if (number == 1)
    {
        return number;
    }

    return 2 * jumpFloorII(number - 1);
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
public List<int> printListFromTailToHead(ListNode listNode)
{
    if (listNode != null)
    {
        printListFromTailToHead(listNode.next);
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
## 链表中倒数第k个结点
输入一个链表，输出该链表中倒数第k个结点。
[牛客](https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=13&tqId=11167&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
// 使用循环数组。
public ListNode FindKthToTail(ListNode head, int k)
{
    if (head == null || k <= 0)
    {
        return null;
    }

    // 定义一个循环数组。
    ListNode[] temp = new ListNode[k];
    ListNode currentNode = head;
    int index = 0;
    while (currentNode != null)
    {
        // 通过把元素循环放入数组不断更新数组。
        index = (index + k) % k;
        temp[index] = currentNode;
        currentNode = currentNode.next;
        // 指向下一个元素。
        index++;
    }

    return temp[(index + k) % k];
}
```
空间复杂度更低的一种解法：
```cs
// 使用快慢两个指针。
public ListNode FindKthToTail(ListNode head, int k)
{
    if (head == null || k <= 0)
    {
        return null;
    }
    
    // 快指针先到达k-1的位置。
    ListNode fastNode = head;
    for (int i = 0; i < k - 1; i++)
    {
        if (fastNode != null)
        {
            fastNode = fastNode.next;
        }
    }
    
    // k大于链表长度时返回null。
    if (fastNode == null)
    {
        return null;
    }

    // 慢指针从头出发。
    ListNode slowNode = head;
    while (fastNode.next != null)
    {
        slowNode = slowNode.next;
        fastNode = fastNode.next;
    }

    return slowNode;
}
```
## 旋转数组的最小数字
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。 例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。 NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。  
[牛客](https://www.nowcoder.com/practice/9f3231a991af4f55b95579b44b7a01ba?tpId=13&tqId=11159&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)
```cs
public int minNumberInRotateArray(int[] rotateArray)
{
    if (rotateArray.Length == 0)
    {
        return 0;
    }

    for (int i = 0; i < rotateArray.Length - 1; i++)
    {
        if (rotateArray[i] > rotateArray[i + 1])
        {
            return rotateArray[i + 1];
        }
    }

    return rotateArray[0];
}
```
## 合并两个排序的链表
输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。  
[牛客](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=13&tqId=11169&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)
```cs
public ListNode Merge(ListNode pHead1, ListNode pHead2)
{
    if (pHead1 == null)
    {
        return pHead2;
    }

    if (pHead2 == null)
    {
        return pHead1;
    }

    // 处理头结点。
    ListNode temp = null;
    if (pHead1.val >= pHead2.val)
    {
        temp = pHead2;
        pHead2 = pHead2.next;
    }
    else
    {
        temp = pHead1;
        pHead1 = pHead1.next;
    }

    // 保存新链表的头结点。
    ListNode newHead = temp;

    // 处理剩余节点。
    while (pHead1 != null && pHead2 != null)
    {
        if (pHead1.val >= pHead2.val)
        {
            temp.next = pHead2;
            pHead2 = pHead2.next;
        }
        else
        {
            temp.next = pHead1;
            pHead1 = pHead1.next;
        }

        temp = temp.next;
    }

    if (pHead1 == null)
    {
        temp.next = pHead2;
    }
    else if (pHead2 == null)
    {
        temp.next = pHead1;
    }

    return newHead;
}
```
## 数组中重复的数字
在一个长度为n的数组里的所有数字都在0到n-1的范围内。 数组中某些数字是重复的，但不知道有几个数字是重复的。也不知道每个数字重复几次。请找出数组中任意一个重复的数字。 例如，如果输入长度为7的数组{2,3,1,0,2,5,3}，那么对应的输出是第一个重复的数字2。  
[牛客](https://www.nowcoder.com/practice/623a5ac0ea5b4e5f95552655361ae0a8?tpId=13&tqId=11203&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public bool duplicate(int[] numbers, int[] duplication)
{
    if (numbers == null || numbers.Length <= 0)
    {
        return false;
    }

    for (int i = 0; i < numbers.Length; i++)
    {
        while (numbers[i] != i)
        {
            if (numbers[i] == numbers[numbers[i]])
            {
                duplication[0] = numbers[i];
                return true;
            }

            Swap(numbers, i, numbers[i]);
        }
    }

    return false;
}

public void Swap(int[] numbers, int i,int j)
{
    int temp = numbers[i];
    numbers[i] = numbers[j];
    numbers[j] = temp;
}
```
另一种实现
```cs
public bool duplicateV2(int[] numbers, int[] duplication)
{
    if (numbers == null || numbers.Length <= 0)
    {
        return false;
    }

    bool[] t = new bool[numbers.Length];
    for(int i = 0; i < numbers.Length; i++)
    {
        if (t[numbers[i]])
        {
            duplication[0] = numbers[i];
            return true;
        }

        t[numbers[i]] = true;
    }

    return false;
}
```
## 构建乘积数组
给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]\*A[1]*...\*A[i-1]\*A[i+1]\*...\*A[n-1]。不能使用除法。  
[牛客](https://www.nowcoder.com/practice/94a4d381a68b47b7a8bed86f2975db46?tpId=13&tqId=11204&tPage=3&rp=3&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking)
```cs
public int[] multiply(int[] A)
{
    if (A == null)
    {
        return null;
    }

    int[] B = new int[A.Length];
    int t = 1;
    // 先计算分割点前面的乘积。
    for (int i = 0; i < A.Length; i++)
    {
        B[i] = t;
        t *= A[i];
    }

    t = 1;
    // 再计算分割点后面的乘积。
    for(int i = A.Length - 1; i >= 0; i--)
    {
        B[i] *= t;
        t *= A[i];
    }

    return B;
}
```
## 二叉树的镜像
```cs
操作给定的二叉树，将其变换为源二叉树的镜像。
二叉树的镜像定义：源二叉树 
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
```
[牛客](https://www.nowcoder.com/practice/564f4c26aa584921bc75623e48ca3011?tpId=13&tqId=11171&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)
```cs
public class TreeNode
{
    public int val;
    public TreeNode left;
    public TreeNode right;
    public TreeNode(int x)
    {
        val = x;
    }
}
public TreeNode Mirror(TreeNode root)
{
    if (root == null)
    {
        return root;
    }

    SwapTreeNode(root);
    Mirror(root.left);
    Mirror(root.right);
    return root;
}

public static void SwapTreeNode(TreeNode node)
{
    TreeNode temp = node.left;
    node.left = node.right;
    node.right = temp;
}
```
