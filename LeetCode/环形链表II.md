# 给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if(head==null) 
            return null;
        ListNode slow=head;
        ListNode fast=head;
        while(fast!=null){
            slow=slow.next;
            if(fast.next!=null){
                fast=fast.next.next;
            }else{
                return null;
            }
            if(slow==fast){
                ListNode ptr=head;
                while(ptr!=slow){
                    ptr=ptr.next;
                    slow=slow.next;
                }
                return ptr;
            }
        }
        return null;
    }
}
```
