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

   leetcode101. 对称二叉树：
   // 写着写着。。。你就发现你写出来了。。。。。。
   class Solution {
      public boolean isSymmetric(TreeNode root) {
      //条件一：根节点相同
      //条件二：左右子树互为镜像
      if(root == null) return true;
      //因为要有两个参数需要被判断，新加一个函数去实现
      return isSymmetricFunc(root.left,root.right);
      }
      public boolean isSymmetricFunc(TreeNode left,TreeNode right){
        if(left == null && right == null) return true;
        if((left == null && right != null) || (left != null && right == null)) return false;
        if(left.val != right.val) return false;
        return isSymmetricFunc(left.right , right.left) && isSymmetricFunc(left.left , right.right);
    }
}