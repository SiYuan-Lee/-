给你一个由 不同 整数组成的数组 nums ，和一个目标整数 target 。请你从 nums 中找出并返回总和为 target 的元素组合的个数。
```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        int [] dp=new int[target+1];
        dp[0]=1;//
        for(int i=1;i<=target;i++){     
            for(int num:nums){
                if(num<=i){//
                    dp[i]+=dp[i-num];// 假设该排列的最后一个元素是 num，则一定有 num≤i，对于元素之和等于 i −num 的每一种排列，在最后添加 num 之后即可得到一个元素之和等于 i 的排列，因此在计算dp[i] 时，应该计算所有的 dp[i−num] 之和。


                }                                 
            }     
        }
        return dp[target];
    }
} 
```
