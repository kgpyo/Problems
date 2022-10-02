```csharp
public class Solution {
    public int[][] KClosest(int[][] points, int k) {
        var ans = new List<int[]>();
        Array.Sort(points, (a, b) => {
            var first = (a[0]*(long)a[0] + a[1]*(long)a[1]);
            var second = b[0]*(long)b[0] + b[1]*(long)b[1];
            //Console.WriteLine(first);
           // Console.WriteLine(second);
            if (first < second) return -1;
            if (first == second) return 0;
            return 1;
        } );

        for(var i = 0; i < k; i++) {
            ans.Add(new int[]{ points[i][0], points[i][1]});
        }
        return ans.ToArray();
    }
}
```
