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
//递归写着写着就出来了
//  递归的难点在于：找到可以递归的点 为什么很多人觉得递归一看就会，一写就废。 或者说是自己写无法写出来，关键就是你对递归理解的深不深。

// 对于此题： 递归的点怎么找？从拿到题的第一时间开始，思路如下：

// 1.怎么判断一棵树是不是对称二叉树？ 答案：如果所给根节点，为空，那么是对称。如果不为空的话，当他的左子树与右子树对称时，他对称

// 2.那么怎么知道左子树与右子树对不对称呢？在这我直接叫为左树和右树 答案：如果左树的左孩子与右树的右孩子对称，左树的右孩子与右树的左孩子对称，那么这个左树和右树就对称。

// 仔细读这句话，是不是有点绕？怎么感觉有一个功能A我想实现，但我去实现A的时候又要用到A实现后的功能呢？

// 当你思考到这里的时候，递归点已经出现了： 递归点：我在尝试判断左树与右树对称的条件时，发现其跟两树的孩子的对称情况有关系。

// 想到这里，你不必有太多疑问，上手去按思路写代码，函数A（左树，右树）功能是返回是否对称

// def 函数A（左树，右树）： 左树节点值等于右树节点值 且 函数A（左树的左子树，右树的右子树），函数A（左树的右子树，右树的左子树）均为真 才返回真

// 实现完毕。。。

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

leetcode108. 将有序数组转换为二叉搜索树

class Solution {
    //递归只管先动手写
    public TreeNode sortedArrayToBST(int[] nums) {
    if(nums == null) return null;
    int left = 0;
    int right = nums.length - 1;
    int mid = nums.length/2;//此举保证平衡性！！！
    //先建立根节点
    TreeNode root = new TreeNode(nums[mid]);
    //左右子树连上，发现需要用到更多的下标参数，现有的只有一个参数做不到，那么新写一个函数去构建，返回左右子树的根
    root.left = buildTree(nums , left , mid - 1);
    root.right = buildTree(nums, mid +1 , right);
    //返回根节点
    return root;
    }

    public TreeNode buildTree(int[] nums , int left , int right){
    if(nums == null) return null;
    //left和right最后会相等然后结束，若这里不加以控制，就会出现left比right大的情况下继续进行
    if (left > right) {
            return null;
        }
    int mid = (left + right) / 2; //此举保证平衡性！！！
    
    TreeNode root = new TreeNode(nums[mid]);
    root.left = buildTree(nums , left , mid - 1);
    root.right = buildTree(nums, mid +1 , right);
    return root;
    }
}