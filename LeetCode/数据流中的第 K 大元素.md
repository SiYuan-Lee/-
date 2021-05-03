设计一个找到数据流中第 k 大元素的类（class）。注意是排序后的第 k 大元素，不是第 k 个不同的元素。

请实现 KthLargest 类：

KthLargest(int k, int[] nums) 使用整数 k 和整数流 nums 初始化对象。
int add(int val) 将 val 插入数据流 nums 后，返回当前数据流中第 k 大的元素。
```java
class KthLargest {
//堆
    PriorityQueue<Integer> data;
    int k;
    public KthLargest(int k, int[] nums) {
        data=new PriorityQueue<Integer>();//最小堆，每次取出的元素都是队列中权值最小的
        this.k=k;
        for(int num:nums){
           add(num);
        } 
    }
    
    public int add(int val) {
        data.offer(val);
        if(data.size()>k){
            data.poll();
        }
        return data.peek();
    }
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * KthLargest obj = new KthLargest(k, nums);
 * int param_1 = obj.add(val);
 */
 ```
