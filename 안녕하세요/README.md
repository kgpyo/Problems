```c#
public class Solution
{
    public int MaximumGroups(int[] grades)
    {
        var total = grades.Length;
        var answer = 0;
        var count = 1;
        while (total > 0)
        {
            total -= count;
            count++;
            if (total >= 0)
            {
                answer++;
            }
        }
        return answer;
    }
}
```
- 시간복잡도
O(N)

- 풀이<br />
숫자를 오름차순으로 정렬하면 아래와 같을 때 <br />
A, B, C, D ....<br /> 
A <= B <= C <= D  이면, A < (B+C) < (D...)가 항상 성립한다. <br />
따라서 1, 2, 3, .. 그룹화 가능한 갯수만 계산하면 된다. <br />

https://leetcode.com/problems/jump-game-ii/
```c#
public class Solution {
    public int Jump(int[] nums) {
		var dp = new List<int>();
        dp.Add(0);
		for(var i = 1; i< nums.Length; i++)
		{
            dp.Add(dp[i-1] + 1);
		}
		
		for(var i = 0; i < nums.Length; i++)
		{
			var jump = nums[i];
			for(var j = 1; j <= jump; j++) {
                var nextStep = j + i;
                if (nextStep < nums.Length) {
                    dp[nextStep] = Math.Min(dp[nextStep], dp[i] + 1);
                }
            }
		}
		return dp[nums.Length-1];
    }
}
```
- 시간 복잡도
O(N^2)

- 풀이<br />
각 index의 값은 점프 할 수 있는 최대 거리이므로, 해당 위치로부터 도달할 수 있는 거리에 최솟값을 계산한다. <br />
dp[도달 가능한 지점] = Min(dp[도달 가능한 지점], dp[현재 위치] + 1)
