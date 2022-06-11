```c#
public interface IOperator {
    void Operation(IList<int> records);
}

public class Plus : IOperator {
    public void Operation(IList<int> records) {
        var size = records.Count - 1;
        records.Add(records[size] + records[size-1]);
    }
}

public class Double : IOperator {
    public void Operation(IList<int> records) {
        var size = records.Count - 1;
        records.Add(records[size] * 2);
    }
}

public class Undo : IOperator {
    public void Operation(IList<int> records) {
        records.RemoveAt(records.Count - 1);
    }
}

public class Solution {
    public int CalPoints(string[] ops) {
        var records = new List<int>();
        foreach(var op in ops) {
            if (int.TryParse(op, out var score)) {
                records.Add(score);
                continue;
            }
            
            IOperator operation = (op) switch {
                    "C" => new Undo(),
                    "D" => new Double(),
                    "+" => new Plus(),
                    _ => throw new NotImplementedException()
            };
            
            operation.Operation(records);
        }
        
        return records.Sum();
    }
}
```


```c#
class Solution {
private:
    double positvePow(double x, long long n) {
        if (n == 0) {
            return 1;
        }
        if (n == 1) {
            return x;
        }
        double temp = myPow(x, n / 2);
        double result = temp * temp;
        if (n % 2 != 0) {
            result = result * x;
        }
        return result;
    }
public:
    double myPow(double x, int n) {
        double result = positvePow(x, n < 0 ? (long long)-1 * n : n);
        if (n<0) {
            result = (double)1/result;
        }
        return result;        
    }
};

```
