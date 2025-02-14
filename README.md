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
  While there exist a student S who don't have any course
    there is a course C that S didn't apply for
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
### Russian Peasant Muntiplication (Algorithm 2)
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
- **Termination** : Since x is a n-bit number and each time x is becoming half of it, reducing 1 bit in each recursive step and hence it will terminate in n-recursive steps
- **Correctness** :
x.y = |  ceil(x/2)(2y)      if x is even
      |  ceil(x/2)(2y) + y  if x is odd
- **Running Time**: 
```
 T(n)=T(n-1)+O(n)
 T(n)<=T(1)+cn+c(n-1)+c(n-2)+....+c(1)
 T(n)<= c'(n(n-1)/2)
```
-So the running time will be O(n^2)
- **Tightness**   : The algorithm is tight enough (observed in RT analysis)

### SPLIT AND MULTIPLY ALGORITHM
- x.y= (10<sup>m</sup>a+b)(10<sup>m</sup>c+d)
- x.y= 10<sup>2m</sup>ab+10<sup>m</sup>(bc+ad)+bd
- so we will have a recursion by finding a,b,c,d then ab,bc,ad,bd
```cpp
int SM(int x,int y,int n){
  if(n==1){return x.y;}
  int m=ceil(n/2);
  int a=ceil(x/pow(10,m));
  int b=ceil(y/pow(10,m));
  int c=ceil(x%pow(10,m));
  int d=ceil(y%pow(10,m));
  int e=SM(a,c,m);
  int f=SM(a,d,m);
  int g=SM(b,c,m);
  int h=SM(b,d,m);
  return pow(10,2*m)e*f+pow(10,*m)(fg+eh)+fh;
}
```
- **Termination** : Each time n divides by 2 and hence it will take log<sub>2</sub>n steps.
- **Running time**: n->n/2(4 times) and n/2->n/4(4times i.e total 16 steps) and goes on
- T(n) <= 4T(n/2)+O(n)
- T(n) <= cn+cn<sup>2</sup>+cn<sup>3</sup>+....+cn<sup>d</sup>
- T(n) <= c.n.2<sup>d+1</sup>
- T(n) <= c'n<sup>2</sup>
- Sadly time complexity is n square :(
- There is a person who tried to prove n<sup>2</sup>-conjecture.
- **n<sup>2</sup>-conjecture** : Any algorithm that multiplies 2 n-bit integers must take &Omega;(n<sup>2</sup>-conjecture) Kolmogorov
- **Kolmogorov** believe n<sup>2</sup>-conjecture and tried proving it
- **Karastuba** has given an idea which makes n-bit multiplication as n<sup>log<sub>2</sub>3</sup> (i.e n<sup>1.58</sup>)
- (a+b).(c+d)-ac-bd = bc+ad
- a+b and c+d can be having more bits than n.So to remove this confusion we can also do : `ac+bd-(a-b)(c-d)` (As it is subtraction number of bits won't increase.
- Here multiply only once and add/sub takes only O(n) time, since we already calculate ac,bd we will do 3 multiplications(reduced by one)
- Hence the new recurrence looks like
  ```
      T(n) = 3T(n/2)+ O(n)
  ```
- This onl solving gives `n<sup>log<sub>2</sub>3</sup>`
- This multiplication of 2 n-bit numbers complexity is further decreased and currently with running time O(nlogn)

## MASTERS THEORM
  ![image](https://github.com/user-attachments/assets/4d620248-35dc-4f34-ad06-3de6a39761a6)
- Masters theorem is generalization for the recurrence relations in the for `T(n) = aT(n/b) + f(n)`
- 1st one takes f(n) steps
- 2nd one takes af(n/b) steps
- 3rd one take a<sup>2</sup>f(n/b<sup>2</sup>)
- And this goes on...Adding all the terms f(n)+af(n/b)+a<sup>2</sup>f(n/b<sup>2</sup>)+...+a<sup>log<sub>b</sub>n</sup>f(n/b<sup>long<sub>b</sub>n</sup>)
- This will give n<sup>log<sub>b</sub>s</sup> + ∑ a<sup>i</sup> f(n/b<sup>i</sup>)
- This can be generalized
- n<sup>log<sub>b</sub>a</sup> is known as **Watershed Function**.
1. If f(n)=O(n<sup>log<sub>b</sub>a+ε</sup>)  -> T(n) = n<sup>log<sub>b</sub>a</sup>      
2. If f(n)=0(n<sup>log<sub>b</sub>a</sup>log<sup>k</sup>) ->T(n) = n<sup>log<sub>b</sub>a</sup>log<sup>k+1</sup>    
3. If f(n)=&Omega;(n<sup>log<sub>b</sub>a-ε</sup>)  -> T(n) = f(n)

![image](https://github.com/user-attachments/assets/907e7b89-60e7-4121-9e06-8304f8ed8121)

## SORTING ALGORITHMS
- **Merge Sort** takes O(nlogn) it has recurrence relation T(n) = 2T(n/2)+O(n)
```Pseudo Code
#Base case
mergeSort(arr)
if arr has less number of elements (like 5-8)
  sort them
divide the array into two parts
mergeSort(first half)
mergesSort(2nd half)
Merge them into one array i.e in O(n) time
```
#### Quick Select:
1. Choose a pivot in the array let's say p
2. Partition them into two parts where first part contains the elements less than p and second one contains the bigger ones.
3. Recursively sort the array
- Worst case our chose pivot can be the first or last one 🥲
- So Quicksort has T(n)=O(n<sup>2</sup>)
- T(n)=T(r-1)+T(n-r)+O(n)
- WC: T(n)=T(n-1)+T(0)+O(n) i.e. T(n)=O(n<sup>2</sup>)
- To reduce this complexity we can do one thing
- Instead of having worst case with 1st element as pivot if we can choose the median of the element in O(n) time then we can have quicksort algo in O(nlogn)
## Divide and Conquer Strategy
- Divide the problem into instances of the same problem of smaller size.
- Recursively solve all the subproblems.
- Combine the solutions of subproblems to get the solution for original problem.
##### QuickSelect for finding median
- Given array of n elements we should find the kth smallest number(number with rank as k)
- So we will do partition and give the ranks and if k<r we will go into 1st oart else the second else return value we got
- But this also turns out to be O(n<sup>2</sup>)
- Lest's see the pseudo code for it first:
  ```
  QuickSelect(arr,k)
    choose a pivot p
    partition them into two parts (A[1,2,.,.,,r-1] and A[r+1,r+2,...,.,n-1])
    if(k<r)
      QuickSelect(A[1,2,.,.,,r-1],k)
    else if(k>r)
    QuickSelect(A[r+1,r+2,r+3,.,.,n-1],k-r)  #k-r coz alreday r elements we know that are lower than k
    else
      return k
  ```
- Though it is better than previous algorithm since it should go to only once rather than two but still the worst case remains the same.
- T(n) = max{T(n-r,T(r-1}+O(n)
- T(n) = T(n-1)+O(n)
- T(n) = O(n<sup>2</sup>) 😐
- Think something different
- So instead of finding median if we are able to find some offset like..pivot is atleast greater than kn (k<1) then running time may reduce
#### MOMSelect
- **Idea** :
- Divide the array into n/5 blocks find median of each block and then make it as array m 
- Find the median of this median M `O(n/5)`
- Now MOMSelect using the pivot we have obtained
- Compare r and k and go to the part where k will be there  `O(7n/10)`
```Pseudo Code
  MOMSelect(arr,k)
    if arr<18
      sort and find median
    else
      m = floor (n/5)
      find median of all n/5 blocks store it in array M
      mom =  MOMSelect(M,m/2)
      r = partition(arr,mom)
      if(k<r)
        MOMSelect(arr[1,2,.,.r),k)
      else if(k>r)
        MOMSelect(arr[r+1,r+2,.,.,.n-1],k-r)
      else
        return k
```
- **Observation** : mom > atleast n/10 (as it is median of all n/5 block medians
- And each of them is 3rd greatest number hence mom > 3n/10 and similarly mom < 3n/10
- T(n) = T(n/5) + T(7n/10) + O(n)
- n/5 for find median of the medians
- 7n/10 is worst case of pivot
- Similar to before but helps in choosing pivot wisely.
  
  ![WhatsApp Image 2025-02-14 at 18 22 49_51cc907e](https://github.com/user-attachments/assets/19a09f07-cd4f-45e5-98a1-fba6d2102811)

  













































