# Dominator

An array A consisting of N integers is given. The dominator of array A is the value that occurs in more than half of the elements of A.

For example, consider array A such that

 A[0] = 3    A[1] = 4    A[2] =  3
 A[3] = 2    A[4] = 3    A[5] = -1
 A[6] = 3    A[7] = 3
The dominator of A is 3 because it occurs in 5 out of 8 elements of A (namely in those with indices 0, 2, 4, 6 and 7) and 5 is more than a half of 8.

Write a function

function solution(A);

that, given an array A consisting of N integers, returns index of any element of array A in which the dominator of A occurs. The function should return −1 if array A does not have a dominator.

For example, given array A such that

 A[0] = 3    A[1] = 4    A[2] =  3
 A[3] = 2    A[4] = 3    A[5] = -1
 A[6] = 3    A[7] = 3
the function may return 0, 2, 4, 6 or 7, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

```javascript
function solution(A) {
    // write your code in JavaScript (Node.js 8.9.4)
    // console.log('A ', A, 'A length ', A.length);
    if(A.length < 1) return -1;
    var dom = [[A[0], 1, 0]];
    for(i = 1; i < A.length; i++){
        // console.log('A[',i,'] = ', A[i]);
        //check if A[i] exists in dominator stack
        // console.log('dominator stack ', dom);
        for(y = 0; y < dom.length; y++){
            // console.log('dom[', y, '][0] ', dom[y][0], ' === A[i]', A[i])
            if(dom[y][0] === A[i]) {
                dom[y][1]++;
                break;
                // console.log('adding dom[y][1]++ ', dom[y][1], 'y ', y);
            } else if(y < dom.length - 1){
                continue;
            }
            else {
                dom.push([A[i], 1, i]);
                // console.log('pushing ', [A[i], 1, i], 'y ', y )
                break;
            }
        }
    }
    var index  = 0;
    var count = 0;
    // console.log('dominator stack ', dom);
    for(x = 0; x < dom.length; x++){
        
        if(dom[x][1] > count){
            index = dom[x][2];
            count = dom[x][1];
            // console.log('index ', index, 'count ', count)
        }
        if(count > (A.length / 2)) return index;
    }
    return -1
}
```
