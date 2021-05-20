给定一个二叉搜索树的根节点 root ，和一个整数 k ，请你设计一个算法查找其中第 k 个最小元素（从 1 开始计数）
```java
class Solution {
    public int kthSmallest(TreeNode root, int k) {
//非递归
        LinkedList<TreeNode> stack=new LinkedList<>();//链表
        while(true){
            while(root!=null){              
                stack.add(root);
                root=root.left;
            }
            root=stack.removeLast();
            
            if(--k==0) return root.val;
            root=root.right;
        }
 
    }
}
```
```java
class Solution {
    List<Integer> arr=new ArrayList<>();
    public void dfs(TreeNode root){
        if(root==null){
            return;
        }
        dfs(root.left);
        arr.add(root.val);
        dfs(root.right);
    }
    public int kthSmallest(TreeNode root, int k) {
//递归写法
        dfs(root); 
        return arr.get(k-1);
    }
}

```
