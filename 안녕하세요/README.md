```c#
using System;
using System.Collections.Generic;

public class Solution {
    public int solution(int n, int k) {
        int answer = 0;
        
        // 진법 변환
        var numbers = new List<long>();
        while (n > 0) {
            numbers.Add(n % k);
            n/=k;
        }
        
        long target = 0;
        for(var i = numbers.Count - 1; i >= 0; i--) {
            if (numbers[i] == 0) {
                if (IsPrime(target)) {
                    answer++;
                }
                target = 0;
            }            
            target = target * 10 + numbers[i];
            
        }
        
        // 소수판별
        if (IsPrime(target)) {
            answer++;
        }
        return answer;
    }
    
    public bool IsPrime(long nums) {
        if (nums == 1 || nums == 0) {
            return false;
        }
        var count = Math.Sqrt(nums);
        for(int i = 2; i <= count; i++) {
            if (nums % i == 0) {
                return false;
            }
        }
        return true;
    }
}
```
