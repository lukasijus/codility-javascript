An integer N is given, representing the area of some rectangle.

The area of a rectangle whose sides are of length A and B is A * B, and the perimeter is 2 * (A + B).

The goal is to find the minimal perimeter of any rectangle whose area equals N. The sides of this rectangle should be only integers.

For example, given integer N = 30, rectangles of area 30 are:

(1, 30), with a perimeter of 62,
(2, 15), with a perimeter of 34,
(3, 10), with a perimeter of 26,
(5, 6), with a perimeter of 22.
Write a function:

function solution(N);

that, given an integer N, returns the minimal perimeter of any rectangle whose area is exactly equal to N.

For example, given an integer N = 30, the function should return 22, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..1,000,000,000].


```javascript
function solution(N) {
    // write your code in JavaScript (Node.js 8.9.4)
    let per = 0;
    let min_per = 2*(1 + N);
    let A = 1;
    for(let A = 1; A < N / 2; A++){
        let B = N / A;
        if(Number.isInteger(B)){
            // console.log('B = ', B)
            per = 2*(A + B);
            if(min_per > per){
                min_per = per;
            }
        }
        if(A > B) return min_per;
    }
    // console.log('per = ', per, 'min per = ', min_per)
    return min_per;
}
```
