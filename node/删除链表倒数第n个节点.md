### 删除链表倒数第n个节点，返回删除后的头结点

> 例如：[1,2,3]  n=1 ---->  [1,2]


### 分析
重点在于找到倒数第n-1个节点，然后把它的next指向下下个节点即可


### 方法一

倒数第n个节点，即正数的第length-n个节点，所以只要确定链表长度，问题就解决了

#### 思路

引入一个哨兵节点，指向头节点来简化某些边界条件下的操作。遍历链表，移动到length-n的位置，然后把length-n的next指向length-n-2即可

#### 代码
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public ListNode removeNthFromEnd(ListNode head,int n){
    //定义哨兵节点，简化边界条件下的操作
    ListNode solder = new ListNode(0);
    solder.next = head;

    ListNode current = head;
    int length=0;
    while(current!=null){
        length++;
        current = current.next;
    }

    ListNode pre = solder;
    for(int i=0;i<length-n;i++){
        pre = pre.next;
    }  

    pre.next = pre.next.next;
    return solder; 
}
```

### 方法二
方法一执行了2*length次遍历，可以使用双指针优化成length次遍历。定义2个指针（first和second），第一个指针指向头结点，第二个指针指向n+1个节点，他们之间相隔n个节点。同时2个指针，他们之间的间隔始终保持为n，当第二个指针为null时，第一个指针距离第二个指针从链表最后一个节点倒数刚好是n个间隔，正好指向倒数第n个节点的前置节点。这种思路非常的巧妙，最好是画个图，加深理解

#### 代码

```java
public ListNode removeNthFromEnd(ListNode head,int n){
    //定义哨兵节点，简化边界条件下的操作
    ListNode solder = new ListNode(0);
    solder.next = head;

    ListNode first = solder;
    ListNode second = solder

    for(int i=0;i<n+1;i++){
        second = second.next;
    }

    while(second!=null){
        second = second.next;
        first = first.next;
    }

    //当seconde指向null时，firt和second相差n个节点
    first.next = first.next.next;
}

```
