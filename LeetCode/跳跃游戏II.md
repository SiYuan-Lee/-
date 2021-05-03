给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

假设你总是可以到达数组的最后一个位置。
## 贪心算法
```java
class Solution {
    public int jump(int[] nums) {
        int len=nums.length;
       
        int maxPosition=0,steps=0,end=0;
        for(int i=0;i<len-1;++i){
            maxPosition=Math.max(maxPosition,i+nums[i]);
            if(i==end){
                end=maxPosition;
                steps++;
            }
        }
        return steps;
        
    }
}
```
