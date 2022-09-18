```javascript
function solution(s) {
    return s.map(convert);
}

function convert(s) {
    const number = [];
    const target = [];
    for(const ch of s) {
        if (number.length === 0) {
            number.push({
                ch,
                count: ch === '1' ? 1 : 0
            })
            continue;
        }
        
        number.push({
            ch,
            count: (ch === '1') ? number[number.length - 1].count + 1 : 0
        })
        
        while (number.length >= 2 && number[number.length - 1].ch === '0' && number[number.length - 2].count >= 2) {
            target.push('1');
            target.push('1');
            target.push('0');
            number.pop(); // 0
            number.pop(); // 1
            number.pop(); // 1
            continue;
        }
    }
    
    const remained = number.map(row => row.ch);
    const idx = remained.reduce((acc, cur, i) => cur === '0' ? i : acc, -1);
    
    let answer = []
    
    for(let i =0; i<remained.length; i++) {
        answer.push(remained[i]);
        if (i === idx) {
            answer = answer.concat(target);
        }
    }
    
    if (idx === -1) {
        answer = target.concat(answer);
    }
    
    
    return answer.join('')
}
```
