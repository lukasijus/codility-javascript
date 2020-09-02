# Nesting

A string S consisting of N characters is called properly nested if:

S is empty;
S has the form "(U)" where U is a properly nested string;
S has the form "VW" where V and W are properly nested strings.
For example, string "(()(())())" is properly nested but string "())" isn't.

Write a function:

function solution(S);

that, given a string S consisting of N characters, returns 1 if string S is properly nested and 0 otherwise.

For example, given S = "(()(())())", the function should return 1 and given S = "())", the function should return 0, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..1,000,000];
string S consists only of the characters "(" and/or ")

```
javascript

/ you can write to stdout for debugging purposes, e.g.
// console.log('this is a debug message');

function solution(S) {
    // write your code in JavaScript (Node.js 8.9.4)
    var counter = 0;
    S = S.split('');
    for(i = 0; i < S.length; i++){
        // console.log('S ', S, 'S.length ', S.length, 'counter ', counter);
        if ( S.length < 1) return 1;
        if ( S.length === 1 ) return 0;
        // console.log('S[',i,']', S[i], 'S[',i + 1,']', S[i + 1]);
        switch(S[i]){
            case '(':
                counter++;
                break;
            case ')':
                counter--;
                break;
        }
        // if(S[i] === '(' && S[i + 1] === ')'){
        //     // console.log('nested element! REMOVING ');
        //     S.splice(i, 2);
        //     i = i - 2; 
        //     continue;
        // } 
        if(counter < 0) return 0; 
        // else console.log('no nested element!');
    }
    if(counter === 0) return 1;
    else return 0;
}
```
