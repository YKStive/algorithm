### 检查链表中是否有环

问题描述：链表的尾节点的next指针是否指向了链表中任意节点，如果是则表示有环

#### 哈希表
初次看到这个问题，最容易想到也是最大众的方法就是利用哈希表，因为哈希表数据不能重复的特性，用来保存遍历到的节点，如果发现要保存的节点在表中存在，说明有环。
```java
public booleab hasCycle(Node head){
    if(head ==null ){
        return false;
    }
    HashSet<Node> set = new HashSet<>();
    while(head!=null){
        if(set.contains(head)){
            return true;
        }
        set.add(head);
        head = head.next;
    }
}
```
这种方法的缺点是空间复杂度是0(n),还有一种非常巧妙的方法能够使空间复杂度降为O(1),就是利用快慢指针


#### 快慢指针
定义连个指针，一个一次移动2步，一个一次移动1步。如果链表有环，那么快慢指针一定会相遇，如果没环，那快指针一定先指向null

```java
public booleab hasCycle(Node head){
    //空节点或者只有一个节点
   if(head==null || head.next==null){
       return false;
   }

   Node slow=head;
   Node fast = head.next;
   while(slow!=fast){
       //没有环，快指针到达尾节点
       if(fast==null || fast.next==null){
           return fasle;
       }
       slow = slow.next;
       fast = fast.next.next;
   }

   return ture;
```