```javascript
function solution(lottos, win_nums) {
    const win = new Set(win_nums);
    const matches = lottos.reduce((acc, cur) => acc + (win.has(cur) ? 1 : 0), 0);
    const zeros = lottos.filter(row => row === 0).length;
    const grades = {
        0: 6,
        1: 6,
        2: 5,
        3: 4,
        4: 3,
        5: 2,
        6: 1
    };
    return [matches + zeros, matches]
        .map(row => grades[row]);
}
```

```javascript
/**
 * @param {string} password
 * @return {boolean}
 */
var strongPasswordCheckerII = function(password) {
    if (!/[a-z]/.test(password)) {
            return false;
        }
        if (!/[A-Z]/.test(password)) {
            return false;
        }
        if (!/[0-9]/.test(password)) {
            return false;
        }
        if (!/[\!\@\#\$\%\^\&\*\(\)\-\+]/.test(password)) {
            return false;
        }
        if (password.length < 8) {
            return false;
        }
        
        return Array.from(password).reduce((acc, ch, i, arr) => arr[i-1] != ch && acc, true);
};
```
