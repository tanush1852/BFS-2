# BFS-2

## Problem 1

Binary Tree Right Side View (https://leetcode.com/problems/binary-tree-right-side-view/)
## Solution 1
class Solution {
   
    public List<Integer> rightSideView(TreeNode root) {
        List<Integer> result=new ArrayList<Integer>();
       if(root==null) return result;
       Queue<TreeNode> q=new LinkedList<>();
       q.add(root);

       while(!q.isEmpty())
       {
        int size=q.size();

        for(int i=0;i<size;i++)
        {   TreeNode curr=q.poll();
            if(i==size-1){
                result.add(curr.val);
            }

            if(curr.left!=null)
            q.add(curr.left);

            if(curr.right!=null)
            q.add(curr.right);
        }
       }
       return result;

    }
}

   


## Problem 2

Cousins in binary tree (https://leetcode.com/problems/cousins-in-binary-tree/)
## Solution 2:
class Solution {
    public boolean isCousins(TreeNode root, int x, int y) {
        if (root == null) return false; // Edge case: empty tree
        
        Queue<TreeNode> q = new LinkedList<>();          // Queue for BFS traversal
        Queue<TreeNode> parentQ = new LinkedList<>();    // Queue to track parents of nodes
        q.add(root);
        parentQ.add(null); // Root has no parent

        while (!q.isEmpty()) {
            int size = q.size(); // Process nodes level by level
            boolean x_found = false, y_found = false;
            TreeNode x_parent = null, y_parent = null;

            for (int i = 0; i < size; i++) {
                TreeNode current = q.poll();
                TreeNode parent = parentQ.poll();

                // Check if the current node matches x or y
                if (current.val == x) {
                    x_found = true;
                    x_parent = parent;
                }
                if (current.val == y) {
                    y_found = true;
                    y_parent = parent;
                }

                // Add children to the queue with their parent information
                if (current.left != null) {
                    q.add(current.left);
                    parentQ.add(current);
                }
                if (current.right != null) {
                    q.add(current.right);
                    parentQ.add(current);
                }
            }

            // If both x and y are found on the same level, check their parents
            if (x_found && y_found) {
                return x_parent != y_parent; // True if parents are different
            }

            // If only one of x or y is found on this level, return false
            if (x_found || y_found) {
                return false;
            }
        }

        return false; // If x or y is not found in the tree
    }
}



