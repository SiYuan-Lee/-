给一非空的单词列表，返回前 k 个出现次数最多的单词。

返回的答案应该按单词出现频率由高到低排序。如果不同的单词有相同出现频率，按字母顺序排序。

```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
//试试大顶堆，全部放入堆中，再弹出k个元素
        HashMap<String,Integer> cnt=new HashMap<>();
        for(String word: words){
            cnt.put(word,cnt.getOrDefault(word,0)+1);         
        }

        PriorityQueue<Map.Entry<String,Integer>> pq=new PriorityQueue<>(new Comparator<Map.Entry<String,Integer>>(){
            public int compare(Map.Entry<String,Integer> entry1,Map.Entry<String,Integer> entry2){
                return entry1.getValue()==entry2.getValue()?entry2.getKey().compareTo(entry1.getKey()):entry1.getValue()-entry2.getValue();
            }
        });
        for(Map.Entry<String,Integer> entry:cnt.entrySet()){
            pq.offer(entry);
            if(pq.size()>k){
                pq.poll();
            }
        }
        List<String> ans=new ArrayList<String>();
        while(!pq.isEmpty()){
            ans.add(pq.poll().getKey());
        }
        Collections.reverse(ans);
        return ans;
    }
}
```
