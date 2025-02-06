# Design & Analysis of Algorithms

## Algorithm
Algorithm is explicit,unambigous,mechanichally-executable sequence of elementary instructions usually intended to accomplish a specific purpose.

## Gale Shapley Algorithm
- This problem is also known as *STABLE MARRIAGE PROBLEM*
- For pairing students and courses.
- Each student gets 1 course and each course will have one student
- **Unstable Pair** : A pair (Si,Cj) is said to be unstable if Si prefers Cj over current alloted course and Cj prefers Si over current alloted student.
- **Stable Matching** : A matching that doesn't have any unstable pair.
  ```Pseudo Code
  While there exist a student *S* who don't have any course
    there is a course *C* that S didn't apply for
      if C has no student
        S gets alloted to C
      else
        if C has Student S2 and prefers S2 over S
          C rejects S
        else
          C ditches S2 //S2 is not alloted to any course now
          C acceptes S
  ```
| C0 | C1 | C2 |  
|----|----|----|
| S0 | S1 | C1 | 
| S1 | S0 | C1 | 
| S2 | S2 | C1 | 

| S0 | S1 | S2 |
|----|----|----|
| C1 | C0 | C0 |
| C0 | C1 | C1 |
| C2 | C2 | C2 |

- Let's go through this example
- S0 prefers C1 so we will assign (S0-C1)
- S1 preferse C0 so we will assign (S1-C0)
- S2 also prefers C0 but C0 prefers S1 over S2 and hence gets rejected
- S2 prefers C1 but C1 prefers S0 over S2 hence gets rejected
- S2 prefers c2 and gets the Course C2 (S2-C2)
- Hence the final pairing is
  1. S1-C0
  2. S0-C1
  3. S2-C2

- **For any algorithm we have to do the 4 steps inorder to prove its functioning**
  1. Termination
  2. Correctness
  3. Running time
  4. Tightness

## Multiplying two n-bit numbers
-Our First algorithm is High School Method which has O(N^2) time complexity
###Russian Peasant Muntiplication (Algorithm 2)
- I/P: x,y
- O/P: x.y
```C++
int PeasantMultiply(int x,int y){
  if(x==0){return 0;}
  if(x==1){return y;}
  int x'=x/2;
  int y'=y*2;
  int p=PeasantMultiply(x',y');
  if(x%2!=0){p=p+y;}
  return p;
}
```
**Termination** : Since x is a n-bit number and each time x is becoming half of it, reducing 1 bit in each recursive step and hence it will terminate in n-recursive steps
**Correctness** :
x.y = |  ceil(x/2)(2y)      if x is even
      |  ceil(x/2)(2y) + y  if x is odd
**Running Time**: 
T(n)=T(n-1)+O(n)
T(n)<=T(1)+cn+c(n-1)+c(n-2)+....+c(1)
T(n)<= c'(n(n-1)/2)
-So the running time will be O(n^2)
**Tightness**   : The algorithm is tight enough (observed in RT analysis)












