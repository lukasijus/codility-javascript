# Binary Gap
A binary gap within a positive integer N is any maximal sequence of consecutive zeros that is surrounded by ones at both ends in the binary representation of N.

For example, number 9 has binary representation 1001 and contains a binary gap of length 2. The number 529 has binary representation 1000010001 and contains two binary gaps: one of length 4 and one of length 3. The number 20 has binary representation 10100 and contains one binary gap of length 1. The number 15 has binary representation 1111 and has no binary gaps. The number 32 has binary representation 100000 and has no binary gaps.

Write a function:

function solution(N);

that, given a positive integer N, returns the length of its longest binary gap. The function should return 0 if N doesn't contain a binary gap.

For example, given N = 1041 the function should return 5, because N has binary representation 10000010001 and so its longest binary gap is of length 5. Given N = 32 the function should return 0, because N has binary representation '100000' and thus no binary gaps.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..2,147,483,647].

```javascript
function binary_gap(N){
	let	count_1 = 0;
	let	count_0 = 0;
	let	count_0_gap = 0;
	let	gaps = [];
	for(i = 0; i < N.toString(2).length; i++) {
		//count 0's in the array
		if(N.toString(2)[i] == '0') {
			count_0++;	
			count_0_gap++;
		}
		//count 1's in the array
		if(N.toString(2)[i] == '1') {
			count_1++;
		}
		if(N.toString(2)[i] == '0' && N.toString(2)[i+1] == '1') {
			gaps.push(count_0_gap);
			count_0_gap = 0;
		}
	}
	if(count_1 < 2 || count_0 < 1) return 0
	return gaps.sort()[gaps.length - 1]
}

console.log(binary_gap(15))
console.log(binary_gap(32))
console.log(binary_gap(1041))

```
