```javascript
function solution(numbers, hand) {
    const positions = {
        1: [0,0],
        2: [0,1],
        3: [0,2],
        4: [1,0],
        5: [1,1],
        6: [1,2],
        7: [2,0],
        8: [2,1],
        9: [2,2],
        '*': [3, 0],
        0: [3,1],
        '#': [3,2]
    }
    const distance = (hand, pad) => {
        const padCoordinate = positions[pad]
        const handCoordinate = positions[hand]
        if (!handCoordinate) {
            return padCoordinate[0] + padCoordinate[1]
        }
        return Math.abs(handCoordinate[0] - padCoordinate[0]) 
            + Math.abs(handCoordinate[1] - padCoordinate[1])
    }
    
    let left = '*'
    let right = '#'
    const answers = numbers.reduce((hands, pad) => {
        if ([1, 4, 7].includes(pad)) {
            left = pad
            return hands + 'L'
        }
        if ([3, 6, 9].includes(pad)) {
            right = pad
            return hands + 'R'
        }
        const leftHand = distance(left, pad)
        const rightHand = distance(right, pad)
        if (leftHand < rightHand) {
            left = pad
            return hands + 'L'
        }
        if (leftHand > rightHand) {
            right = pad
            return hands + 'R'
        }
        if (hand === 'right') {
            right = pad
            return hands + 'R'
        } else {
            left = pad
            return hands + 'L'
        }
    }, '')
    
    return answers;
}
```
