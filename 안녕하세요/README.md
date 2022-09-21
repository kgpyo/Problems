https://school.programmers.co.kr/learn/courses/30/lessons/42890

비트 연산자로 모든 경우의 수 다 확인

```javascript
function solution(relation) {
    const answer = [];
    for(let candidate = 1; candidate < (1 << relation[0].length); candidate++) {
        // 유일성 찾기
        let isCandidate = true;
        const set = new Set();
        for(let row = 0; row < relation.length; row++) {
            const record = relation[row]
                .filter((_, col) => ((1 << (col)) & candidate) !== 0)
                .join(',')
            
            if (set.has(record)) {
                isCandidate = false
                break;
            }
            set.add(record)
        }
        
        // 최소성 찾기
        if (isCandidate && !answer.some(row => (row & candidate) == row)) {
            answer.push(candidate)
        }
    }
    return answer.length;
}
```

https://leetcode.com/problems/island-perimeter/
```c#
public class Solution {
    
    private readonly int[][] direction = new int[][] {
        new int[] {0, 1},
        new int[] {0, -1},
        new int[] {1, 0},
        new int[] {-1, 0}
    };
    
    private int Visit(int[][] grid, bool[][] visit, int startRow, int startCol) {
        var perimeter = 0;
        
        var queue = new Queue<(int, int)>();
        queue.Enqueue((startRow, startCol));
        
        
        while (queue.Count > 0) {
            var (row, col) = queue.Dequeue();
            
            for(int i = 0; i < 4; i++) {
                var nr = row + this.direction[i][0];
                var nc = col + this.direction[i][1];
                
                
                
                if (nr < 0 || nc < 0 || nr >= grid.Length || nc >= grid[0].Length) {
                    perimeter++;
                    continue;
                }
                        
                if (grid[nr][nc] == 0) {
                    perimeter++;
                    continue;
                }
                
                if (visit[nr][nc]) {
                    continue;
                }
                
                visit[nr][nc] = true;
        
                
                queue.Enqueue((nr, nc));
            }
        }
        
        return perimeter;
    }
    
    public int IslandPerimeter(int[][] grid) {
        var count = 0;
        var visit = new bool[grid.Length][];
        for(int i = 0; i < grid.Length; i++) {
            visit[i] = new bool[grid[i].Length];
        }
        
        for(int i = 0; i < grid.Length; i++) {
            for(int j = 0; j < grid[i].Length; j++) {
                if (visit[i][j] == false && grid[i][j] == 1) {
                    visit[i][j] = true;
                    count += Visit(grid, visit, i, j);
                }
            }
        }
        return count;
    }
}
```
