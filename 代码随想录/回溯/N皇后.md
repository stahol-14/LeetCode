# [N皇后](N皇后"[题目地址](https://leetcode.cn/problems/n-queens/description/)")

## 题目描述

按照国际象棋的规则，皇后可以攻击与之处在同一行或同一列或同一斜线上的棋子。

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。

每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

 

### 思路：回溯🌟

- 记录 列：在某一列（放置皇后的列）
- 记录 主对角线：row - col
- 记录 副对角线：row + col


```java
class Solution {
    // n皇后问题：不能在 同一行、同一列、同一斜线（主副对角线）
    // 采用 回溯的方式 每层为n 每列为n 进行穷举

    List<List<String>> result = new ArrayList<>(); // 存结果
    List<Integer> path = new ArrayList<>(); // 存在第几列（每行放置的列索引）

    public List<List<String>> solveNQueens(int n) {

        Set<Integer> columns = new HashSet<>(); // 记录 在某一列（放置皇后的列）
        Set<Integer> diag1 = new HashSet<>(); // 记录 在主对角线 row - col
        Set<Integer> diag2 = new HashSet<>(); // 记录在 副对角线 row + col

        backtracking(n, 0, columns, diag1, diag2); // 从第0行开始 遍历到最后一行
        return result;
    }

    private void backtracking(int n, int row, Set<Integer> columns, Set<Integer> diag1, Set<Integer> diag2){

        if(row == n){
            // 递归到最后一行
            result.add(buildBoard(path, n));
            return ;
        }

        for(int col = 0; col < n; col++){
            // 冲突判断：列 或 对角线 冲突
            if (columns.contains(col) || diag1.contains(row - col) || diag2.contains(row + col)) {
                continue;
            }

            // 做选择：放置皇后
            path.add(col); // 加入该列
            columns.add(col); // 记录列的下标
            diag1.add(row - col); // 记录该皇后的主对角线值
            diag2.add(row + col); // 记录该皇后的副对角线值

            // 进入下一层
            backtracking(n, row + 1, columns, diag1, diag2);

            // 撤销选择（回溯）
            path.remove(path.size() - 1);
            columns.remove(col);
            diag1.remove(row - col);
            diag2.remove(row + col);
        }
    }

    private List<String> buildBoard(List<Integer> path, int n){
        List<String> board = new ArrayList<>();
        for(int col : path){ // 遍历每一行皇后所在的列
            char[] row = new char[n];
            Arrays.fill(row, '.');
            row[col] = 'Q';
            board.add(new String(row));
        }
        return board;
    }
}
```
----

不使用额外的数据结构，直接判断棋盘上的字符位置

```java
class Solution {

    public List<List<String>> solveNQueens(int n) {
        List<List<String>> res = new ArrayList<>();

        // 初始化棋盘，全部填充为 '.'
        char[][] board = new char[n][n];
        for(int i = 0; i < n; i++){
            Arrays.fill(board[i], '.');
        }

        // 从第0行开始放置皇后
        backtrack(res, board, 0, n);
        return res;
    }

    /**
     * 回溯函数：尝试在当前 row 行放置皇后
     * @param res   存储所有合法结果
     * @param board 当前棋盘状态
     * @param row   当前行号
     * @param n     棋盘大小
     */
    private void backtrack(List<List<String>> res, char[][] board, int row, int n){
        // 如果已经放置完所有行，说明找到一个合法解
        if(row == n){
            res.add(generateBoard(board)); // 将棋盘转换为字符串形式
            return;
        }

        // 尝试在当前行的每一列放置皇后
        for(int j = 0; j < n; j++){
            if(isValid(board, row, j, n)){
                board[row][j] = 'Q'; // 放置皇后
                backtrack(res, board, row + 1, n); // 递归下一行
                board[row][j] = '.'; // 回溯，移除皇后
            }
        }
    }

    /**
     * 判断在 (row, col) 是否可以放置皇后
     */
    private boolean isValid(char[][] board, int row, int col, int n){
        // 检查列方向是否有皇后
        for(int i = 0; i < row; i++){
            if(board[i][col] == 'Q'){
                return false;
            }
        }

        // 检查左上对角线是否有皇后
        for(int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--){
            if(board[i][j] == 'Q'){
                return false;
            }
        }

        // 检查右上对角线是否有皇后
        for(int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++){
            if(board[i][j] == 'Q'){
                return false;
            }
        }

        return true; // 当前点合法
    }

    /**
     * 将当前棋盘 char[][] 转换为字符串列表
     */
    private List<String> generateBoard(char[][] board) {
        List<String> result = new ArrayList<>();
        for (char[] row : board) {
            result.add(new String(row)); // 将 char[] 转换为 String
        }
        return result;
    }
}
```


#### 复杂度分析
时间复杂度：
空间复杂度：

### 总结
