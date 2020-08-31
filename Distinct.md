# Distinct
Write a function

function solution(A);

that, given an array A consisting of N integers, returns the number of distinct values in array A.

For example, given array A consisting of six elements such that:

 A[0] = 2    A[1] = 1    A[2] = 1
 A[3] = 2    A[4] = 3    A[5] = 1
the function should return 3, because there are 3 distinct values appearing in array A, namely 1, 2 and 3.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
each element of array A is an integer within the range [−1,000,000..1,000,000].

```javascript
// you can write to stdout for debugging purposes, e.g.
// console.log('this is a debug message');
function solution(A) {
    // write your code in JavaScript (Node.js 8.9.4)
    A = A.sort()
    return A.reduce((acc, curr, i , s) => {
        // console.log('acc ', acc, 'curr ', curr, 's[i - 1]', s[i -1], 'i ', i, 's ', s)
        if(s[i +1] !== curr) {
            return acc + 1;
        } 
        else return acc;
    }, 0)
}
```
