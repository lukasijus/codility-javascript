# Brackets
A string S consisting of N characters is considered to be properly nested if any of the following conditions is true:

S is empty;
S has the form "(U)" or "[U]" or "{U}" where U is a properly nested string;
S has the form "VW" where V and W are properly nested strings.
For example, the string "{[()()]}" is properly nested but "([)()]" is not.

Write a function:

function solution(S);

that, given a string S consisting of N characters, returns 1 if S is properly nested and 0 otherwise.

For example, given S = "{[()()]}", the function should return 1 and given S = "([)()]", the function should return 0, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..200,000];
string S consists only of the following characters: "(", "{", "[", "]", "}" and/or ")".

```javascript

function solution(S) {
    // write your code in JavaScript (Node.js 8.9.4)
    // console.log('S ', S);
    var set = S;
    if(S.length < 1) return 1
    var counter = 0;
    var l1_count = 0, l2_count = 0, l3_count = 0;
    var l1 = "(", r1 = ")", l2 = "{", r2 = "}", l3 = "[", r3 = "]";
    if(S[0] === r1 || S[0] === r2 || S[0] === r3) return 0;
    for(i = 0; i < S.length; i++){
        // console.log('S[',i,'] is ', S[i])
        switch(S[i]){
            case l1:
                l1_count++;
                break;
            case l2:
                l2_count++;
                break;
            case l3:
                l3_count++;
                break;
            case r1:
                l1_count--;
                break;
            case r2:
                l2_count--;
                break;
            case r3:
                l3_count--;
                break;
        }
        if(S[i] === l1){
            // console.log('search for ', r1);
            //l1, l2, l3 and r1 is ok else return 0
            if(S[i + 1] === r2 || S[i + 1] === r3){
                return 0
            }
        }
        if(S[i] === l2){
            // console.log('search for ', r2);
            //l1, l2, l3 and r2 is ok else return 0
            if(S[i + 1] === r1 || S[i + 1] === r3){
                return 0
            }
        }
        if(S[i] === l3){
            // console.log('search for ', r3);
            //l1, l2, l3 and r3 is ok else return 0
            if(S[i + 1] === r1 || S[i + 1] === r2){
                return 0
            }
        } 
    }
    if(l1_count !== 0 || l2_count !== 0 || l3_count !== 0) return 0;
    return 1
}
```
