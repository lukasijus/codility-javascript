# Missing Integer
This is a demo task.

Write a function:

function solution(A);

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
each element of array A is an integer within the range [−1,000,000..1,000,000].
```javascript
function solution(A) {
    // write your code in JavaScript (Node.js 8.9.4)
    // Filter positive
    A = A.filter(i => (i > 0))

    // sort arrays
    A.sort()

    if (A.length == 1 && A[0] === 1) {
        return 2
    }
    
    if (A[0] !== 1) return 1
    
    for (var i=1; i<A.length; i++) {
        if ((A[i] - A[i-1]) > 1) {
            return A[i-1] + 1
        }
    }
    return A[A.length - 1] + 1
}
```
