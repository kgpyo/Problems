- O(n^n)
```csharp
using System;

public class Solution {
    private readonly int[,] dir = new int[,] { {0,1},{0,-1},{1,0},{-1,0}, {-1,-1},{-1,1},{1,1},{1,-1} };
    
    public int solution(int[,] board) {
        int answer = 0;
        
        for (int i = 0; i < board.GetLength(0); i++) {
            for(int j = 0; j < board.GetLength(1); j++) {
                if (board[i,j] == 1) {
                    for(int k = 0; k < dir.GetLength(0); k++) {
                        int ni = i + dir[k, 0];
                        int nj = j + dir[k, 1];
                        
                        if (ni < 0 || nj < 0 || ni >= board.GetLength(0) || nj >= board.GetLength(1)) {
                            continue;
                        }
                        if (board[ni,nj] != 0) {
                            continue;
                        }
                        board[ni,nj] = -1;
                    }
                }
            }
        }
        
        for(int i = 0; i < board.GetLength(0); i++) {
            for (int j = 0; j< board.GetLength(1); j++) {
                if (board[i,j] == 0) {
                    answer++;
                }
            }
        }
        
        return answer;
    }
}
```
```csharp
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    private int GetRank(TreeNode cur, int rank)
    {
        int next = 0;
        if (cur.left is not null) {
            next = GetRank(cur.left, rank) + 1;
        }
        if (cur.right is not null) {
            next = Math.Max(next, GetRank(cur.right, rank) + 1);
        }

        if (cur.left is null && cur.right is null) {
            return 1;
        }

        return next;
    }

    private int GetSum(TreeNode cur, int rank) {
        if (cur.left is null && cur.right is null) {
            return rank == 0 ? cur.val : 0;
        }

        int sum = 0;
        if (cur.left is not null) {
            sum += GetSum(cur.left, rank-1);
        }
        if (cur.right is not null) {
            sum += GetSum(cur.right, rank-1);
        }

        return sum;
    }
    
    public int DeepestLeavesSum(TreeNode root) {
        var rank = GetRank(root, 0);
        return GetSum(root, rank - 1);
    }
}
```
