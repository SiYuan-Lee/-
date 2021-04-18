
你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都 围成一圈 ，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警 。

给定一个代表每个房屋存放金额的非负整数数组，计算你 在不触动警报装置的情况下 ，今晚能够偷窃到的最高金额。

```java
class Solution {
    public int rob(int[] nums) {
        int len=nums.length;
        int []DP=new int[len];
        if(len==1) return nums[0];
        if(len==2) return Math.max(nums[0],nums[1]);
        int max1=0,max2=0;
        DP[0]=nums[0];
        DP[1]=Math.max(nums[0],nums[1]);
        for(int i=0;i<len-1;i++){
            if(i>1){
                DP[i]=Math.max(DP[i-1],DP[i-2]+nums[i]);
            }
            
            max1=Math.max(DP[i],max1);
        }
        DP[1]=nums[1];
        DP[2]=Math.max(nums[1],nums[2]);
        for(int i=1;i<len;i++){
            if(i>2){
                DP[i]=Math.max(DP[i-1],DP[i-2]+nums[i]);
            }
            
            max2=Math.max(DP[i],max2);
        }
        return Math.max(max1,max2);
    }
}
```
