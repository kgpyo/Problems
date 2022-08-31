## https://leetcode.com/problems/4sum/

- 입력 범위가 200이므로 단순 반복문 사용시 O(n^4) => 1600000000 (약 16초)
- 숫자를 미리 정렬한 후 Two sum 문제로 분해해서 푼다.
- 시간복잡도 O(n^3)
  - two pointer를 이용한 two sum의 시간복잡도는 O(n)
  - two sum 을 호출 할때 반복문의 시간복잡도는 O(n^2)
- int 범위를 넘어설 수 있다. (num 원소 값 하나가 10^9까지 가능)


```csharp
public class Solution {
    public IList<IList<int>> FourSum(int[] nums, int target) {
        Array.Sort(nums);        
        // 1 , 2 ,3 ,4, 5
        // 0 0 0 0
        var answer = new List<IList<int>>();
        for(var i = 0; i < nums.Length; i++) {
            var a = nums[i];
            if ( i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            for(var j = i + 1; j < nums.Length; j++) {
                if (j > i + 1 && nums[j] == nums[j-1]) {
                    continue;
                }
                
                var b = nums[j];
                var subTarget = (long)target - (a + b);
                
                var left = j + 1;
                var right = nums.Length - 1;
                
                while(left < right) {
                    var subSum = (long)nums[left] + nums[right];
                    if (subSum > subTarget || (right < nums.Length - 1 && nums[right] == nums[right + 1])) {
                        right--;
                    } else if (subSum < subTarget || (left > j + 1 && nums[left] == nums[left - 1])) {
                        left++;
                    } else {
                        answer.Add(new List<int> {a, b, nums[left], nums[right]});
                        left++;
                        right--;
                    }
                }
                
            }
        }
        
        return answer;
    }
}
```

## https://leetcode.com/problems/3sum/
- 동일 문제 선택
```csharp
public class Solution {
    public IList<IList<int>> ThreeSum(int[] nums) {
        var answer = new List<IList<int>>();
        Array.Sort(nums);
        for(var i = 0; i < nums.Length; i++) {
            if (i > 0 && nums[i] == nums[i-1]) {
                continue;
            }
            
            var a = nums[i];
            
            var left = i + 1;
            var right = nums.Length - 1;
            while(left < right) {
                var sum = a + nums[left] + nums[right];
                
                if (sum < 0 || (left > i + 1 && nums[left] == nums[left - 1])) {
                    left++;
                } else if (sum > 0 || (right < nums.Length - 2 && nums[right] == nums[right+1])) {
                    right--;
                } else {
                    answer.Add(new List<int> {a, nums[left], nums[right]});
                    left++;
                    right--;
                }
            }
            
        }
        
        return answer;
    }
}
```
