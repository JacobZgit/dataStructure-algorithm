leetcode给的模板函数不太好处理，于是在这个模板函数里调用另外一个我们自己写的函数

leetcode94. 二叉树的中序遍历：
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> list= new ArrayList<Integer>();
        inorder(root,list);
        return list;
    }
    public void inorder(TreeNode root, List list){
        if(root == null) return;
        inorder(root.left,list);
        list.add(root.val);
        inorder(root.right,list);
    }
}