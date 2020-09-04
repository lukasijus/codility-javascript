# Equi Leaders

A non-empty array A consisting of N integers is given.

The leader of this array is the value that occurs in more than half of the elements of A.

An equi leader is an index S such that 0 ≤ S < N − 1 and two sequences A[0], A[1], ..., A[S] and A[S + 1], A[S + 2], ..., A[N − 1] have leaders of the same value.

For example, given array A such that:

    A[0] = 4
    A[1] = 3
    A[2] = 4
    A[3] = 4
    A[4] = 4
    A[5] = 2
we can find two equi leaders:

0, because sequences: (4) and (3, 4, 4, 4, 2) have the same leader, whose value is 4.
2, because sequences: (4, 3, 4) and (4, 4, 2) have the same leader, whose value is 4.
The goal is to count the number of equi leaders.

Write a function:

function solution(A);

that, given a non-empty array A consisting of N integers, returns the number of equi leaders.

For example, given:

    A[0] = 4
    A[1] = 3
    A[2] = 4
    A[3] = 4
    A[4] = 4
    A[5] = 2
the function should return 2, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
each element of array A is an integer within the range [−1,000,000,000..1,000,000,000].

```javascript
function solution1(A){
	// console.log('A', A);
	var start_time = new Date();
	var equi_leader = 0;
	var curr_el = 0;
	for(i = 0; i < A.length; i++){
//		console.log('A[',i,'] = ', A[i])
//		console.log(stack.includes(A[i]));
		var seq1 = A.slice(0, i + 1);
		var seq2 = A.slice(i + 1, A.length);
		// console.log('sequence 1 ' , seq1, 'sequence 2 ' , seq2);
		var seq1_max_count = 0;
		var seq1_number;
		var seq1_leader = false;
		var seq2_max_count = 0;
		var seq2_number;
		var seq2_leader = false;
		for(j = 0; j < Math.max(seq1.length, seq2.length); j++){
			// console.log('seq1[',j,'] = ', seq1[j]);
			// console.log('seq2[',j,'] = ', seq2[j]);
			var seq1_count = 0;
			var seq2_count = 0;
			for (let k = 0; k < Math.max(seq1.length, seq2.length); k++) {
				// if((seq1[j] === undefined || seq2[j] === undefined )){
				// 	console.log('seq1[',j,'] = ', seq1[j]);
				// 	console.log('seq2[',j,'] = ', seq2[j]);
				// 		console.log('break!')
				// 		break;
				// 	}
				if(seq1[j] === seq1[k]){
					seq1_count++;
				}
				if(seq1_count > seq1_max_count){
	//				console.log('change from', number, 'to ' , A[i]);
					seq1_max_count = seq1_count;
				}
				if(seq1_max_count > seq1.length/2 && !seq1_leader) {
					seq1_leader = true;
					seq1_number = seq1[j];
					//console.log('leader in seq1 is', seq1_number,  'occurs ', seq1_max_count, 'time');
				}
				//console.log('after seq 1', 'seq2[',j, '] = ', seq2[j], 'seq2[',k, '] = ', seq2[k], 'seq2_count = ', seq2_count, 'seq2_number ', seq2_number);
				if(seq2[j] === seq2[k]){
					//console.log('count seq2 count');
					seq2_count++;
				}
				if(seq2_count > seq2_max_count){
	//				console.log('change from', number, 'to ' , A[i]);
					seq2_max_count = seq2_count;
				}
				if(seq2_max_count > seq2.length/2 && !seq2_leader) {
					//console.log('leader in seq2 is', seq2_number,  'occurs ', seq2_max_count, 'time');
					seq2_leader = true;
					seq2_number = seq2[j];
				}
				if(seq1_leader && seq2_leader && (seq1_number ===  seq2_number)){
					// console.log('equi leader!')
					equi_leader++;
					break;
				}
			} //console.log('2nd for loop end');
			if(equi_leader > curr_el){
				curr_el = equi_leader;
				break;
			}
		}	
	} 
	var end_time = new Date();
	var time_diff = Math.round((end_time - start_time) * 1000)/ 1000;
	return [time_diff, equi_leader];
}
	


function solution2(A) {
	var start_time = new Date();
    var pos = 0;
    var count = 0;
	// console.log('A ', A );
    for (var i = 0; i < A.length; i++) {
		// console.log('A[',i,'] = ', A[i], 'pos = ', pos, 'A[pos] = ', A[pos], 'count = ', count, ' is A[ ',pos, '] == A[', i, ']', A[pos] == A[i]);
        if (A[pos] == A[i]) {
			count++;
			// console.log('if true count++ ', count);
        } else {
			count--;
			// console.log('if false count-- ', count);
            if (count == 0) {
				// console.log('change max number from A[',pos,'] = ', A[pos], ' to A[',i,'] = ', A[i]);
                pos = i;
				count++;
            }
        }
    }
	// console.log('pos = ', pos, 'A[', pos, '] = ', A[pos]);
    var ret = 0;
    var cand = A[pos];

    var E = [];
    var N = [];

    var ec = 0;
    var nc = 0;
    for (var i = 0; i < A.length; i++) {
		// console.log('E ', E, 'N ', N)
        if (A[i] == cand) {
            ec++;
        } else {
            nc++;
        }
        E[i] = ec;
        N[i] = nc;
    }

    for (var i = 0; i < A.length; i++) {
		// console.log('E[i] = ', E[i], 'N[i] = ',N[i],  '((nc - N[i]) = ',((nc - N[i]),  '(ec - E[i]) = ', (ec - E[i])));
        if (E[i] > N[i] && ((nc - N[i]) < (ec - E[i]))) {
			ret++;
			// console.log('ret = ', ret);
        }
    }

    var end_time = new Date();
	var time_diff = Math.round((end_time - start_time) * 1000)/ 1000;
	return [time_diff, ret];
}


var Arr = Array.from({length: 1000}, () => Math.floor(Math.random() * 2));
console.log(solution1(Arr));
console.log(solution2(Arr));
console.log(solution1([4,3,4,4,4,2]));
console.log(solution2([4,3,4,4,4,2]));
console.log(solution1([4,3,4,4,3, 4,2, 3, 3, 3, 4, 4	]));
console.log(solution2([4,3,4,4,3, 4,2, 3, 3, 3, 4, 4	]));
```
