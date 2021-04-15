设计和构建一个“最近最少使用”缓存，该缓存会删除最近最少使用的项目。缓存应该从键映射到值(允许你插入和检索特定键对应的值)，并在初始化时指定最大容量。当缓存被填满时，它应该删除最近最少使用的项目。

它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。当缓存容量达到上限时，它应该在写入新数据之前删除最近最少使用的数据值，从而为新的数据值留出空间。

```java
class LRUCache {
    class DlinkedNode{
        int key;
        int val;
        DlinkedNode prev;
        DlinkedNode next;
        public DlinkedNode(){};
        public DlinkedNode(int _key,int _val){key=_key;val=_val;}
    }//定义双向链表节点结构
    HashMap<Integer,DlinkedNode> cache=new HashMap<>();//哈希表，存储密钥和和双向链表密钥节点的映射
    private int size;
    private int capacity;
    DlinkedNode head;//伪头节点
    DlinkedNode tail;//伪尾节点
    public LRUCache(int capacity) {
        this.size=0;
        this.capacity=capacity;
        head=new DlinkedNode();
        tail=new DlinkedNode();
        head.next=tail;
        tail.prev=head;
    }//初始化缓存区大小，初始化头尾节点
    
    public int get(int key) {//获取数据
        DlinkedNode node=cache.get(key);
        if(node==null) return -1;//缓存区不存在密钥
        movetoHead(node);//因为使用了一次，所以当前节点移动到头部，表示最近一次使用过
        return node.val;//存在密钥，从哈希表中获取
    }
    
    public void put(int key, int value) {//写入数据
        DlinkedNode node=cache.get(key);
        if(node==null){//如果节点不存在
            DlinkedNode newnode=new DlinkedNode(key,value);  //创建一个节点，存储密钥 ，根据最近使用顺序排列密钥，越近使用的，排在最前面    
            cache.put(key,newnode);//放入哈希表，方便查询密钥对应的双向链表节点，从而删除或者更改密钥的存储位置
            addToHead(newnode);//放入双向链表
            ++size;
            if(size>capacity){
                DlinkedNode tail=removeTail();
                cache.remove(tail.key);
                --size;//超过缓存区大小，删除链表尾部的节点，为了节省空间，删的原则是最久没有使用的
            }
        }else{
            node.val=value;
            movetoHead(node);//更新密钥值，放到头节点

        }
    }
    public void addToHead(DlinkedNode node){
        head.next.prev=node;
        node.prev=head;
        node.next=head.next;
        head.next=node;
    }
    public void removenode(DlinkedNode node){
        node.prev.next=node.next;
        node.next.prev=node.prev;
    }
    public void movetoHead(DlinkedNode node){
        removenode(node);
        addToHead(node);
    }
    public DlinkedNode removeTail(){
        DlinkedNode res=tail.prev;
        removenode(res);
        return res;
    }
}


/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
 ```
