动态规划
```JAVA
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    Map<TreeNode, Integer> f=new HashMap<TreeNode,Integer>();
    Map<TreeNode, Integer> g=new HashMap<TreeNode,Integer>();
    public void dfs(TreeNode node){
        if(node==null){
            return;
        }
        dfs(node.left);
        dfs(node.right);
        f.put(node,node.val+g.getOrDefault(node.left,0)+g.getOrDefault(node.right,0));
        g.put(node,Math.max(f.getOrDefault(node.left,0),g.getOrDefault(node.left,0))+Math.max(f.getOrDefault(node.right,0),g.getOrDefault(node.right,0)));
    }
    public int rob(TreeNode root) {  
        dfs(root);           
        return Math.max(f.getOrDefault(root,0),g.getOrDefault(root,0));
    }
}
```
