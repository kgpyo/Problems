```csharp
public class Solution {

    private bool IsValidSudoku(char[] board) {
        bool[] used = new bool[10];
        for(int i = 0; i < 9; i++) {
            if (board[i] == '.') {
                continue;
            }
            var cur = board[i] - '0';
            if (used[cur]) {
                return false;
            }
            used[cur] = true;
        }

        return true;
    }

    public bool IsValidSudokuRow(char[][] board) {
        for(int row = 0; row < 9; row++) {
            if (IsValidSudoku(board[row]) is false) {
                return false;
            }
        }
        return true;
    }

    public bool IsValidSudokuCol(char[][] board) {
        for(int col = 0; col < 9; col++) {
            if (IsValidSudoku(board.Select(row => row[col]).ToArray()) is false) {
                return false;
            }
        }
        return true;  
    }

    public bool IsValidSudokuArea(char[][] board) {
        for(int row = 0; row < 9; row+=3) {
            for(int col = 0; col < 9; col+=3) {

                bool[] used = new bool[10];
                for(int i = 0; i < 3; i++) {
                    for(int j = 0; j< 3; j++) {
                        var cur = board[row+i][col+j];
                        if (cur == '.') {
                            continue;
                        }
                        if (used[cur-'0']) {
                            return false;
                        }
                        used[cur-'0'] = true;
                    }
                }

            }
        }

        return true;
    }

    public bool IsValidSudoku(char[][] board) {
        return 
        IsValidSudokuRow(board) 
        && IsValidSudokuCol(board)
        && IsValidSudokuArea(board);
    }
}
```
