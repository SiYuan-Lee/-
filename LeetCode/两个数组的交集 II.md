给定两个数组，编写一个函数来计算它们的交集。
```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
//hashmap
        int l1=nums1.length;
        int l2=nums2.length;
        int []ans=new int[Math.min(l1,l2)];  
        HashMap<Integer,Integer> map=new HashMap<>();    
        for(int num:nums2){
            map.put(num,map.getOrDefault(num,0)+1);
        }
        int index=0;
        for(int num:nums1){
            if(map.containsKey(num)){               
                map.put(num,map.get(num)-1); 
                if(map.get(num)==0){
                    map.remove(num);
                }             
                ans[index++]=num;                                                         
            }          
        }
        return Arrays.copyOfRange(ans, 0, index);
    }
}
```
