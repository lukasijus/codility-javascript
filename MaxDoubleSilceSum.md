A non-empty array A consisting of N integers is given.

A triplet (X, Y, Z), such that 0 ≤ X < Y < Z < N, is called a double slice.

The sum of double slice (X, Y, Z) is the total of A[X + 1] + A[X + 2] + ... + A[Y − 1] + A[Y + 1] + A[Y + 2] + ... + A[Z − 1].

For example, array A such that:

    A[0] = 3
    A[1] = 2
    A[2] = 6
    A[3] = -1
    A[4] = 4
    A[5] = 5
    A[6] = -1
    A[7] = 2
contains the following example double slices:

double slice (0, 3, 6), sum is 2 + 6 + 4 + 5 = 17,
double slice (0, 3, 7), sum is 2 + 6 + 4 + 5 − 1 = 16,
double slice (3, 4, 5), sum is 0.
The goal is to find the maximal sum of any double slice.

Write a function:

function solution(A);

that, given a non-empty array A consisting of N integers, returns the maximal sum of any double slice.

For example, given:

    A[0] = 3
    A[1] = 2
    A[2] = 6
    A[3] = -1
    A[4] = 4
    A[5] = 5
    A[6] = -1
    A[7] = 2
the function should return 17, because no double slice of array A has a sum of greater than 17.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [3..100,000];
each element of array A is an integer within the range [−10,000..10,000].

```javascript
function solution(A) {
    // write your code in JavaScript (Node.js 8.9.4)
    const N = A.length;
    if(N === 3) return 0;
    let max_sum_end = new Array(N).fill(0);
    let max_sum_start = new Array(N).fill(0);
    for(let i = 1; i < (N - 1); i++){
        max_sum_end[i] = Math.max(0, max_sum_end[i - 1] + A[i]);
    }
    
    for(let k = N - 2; k > 0; k--){
        max_sum_start[k] = Math.max(0, max_sum_start[k + 1] + A[k])
    }
    
    let maxvalue = 0;
    let temp = 0;
    // console.log('max_sum_end = ', max_sum_end, 'max_sum_start = ', max_sum_start);
    for(let y = 1; y < (N -1); y++){
        temp =  max_sum_end[y - 1] + max_sum_start[y + 1];
        if(temp > maxvalue) {
            maxvalue = temp;
        }
    }
    
    return maxvalue;
}
```
