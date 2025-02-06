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
|----|----|----|      
| S1 | S0 | C1 |       
|----|----|----|       
| S2 | S2 | C1 | 

| S0 | S1 | S2 |
|----|----|----|   
| C1 | C0 | C0 |
|----|----|----| 
| C0 | C1 | C1 |
|----|----|----|
| C2 | C2 | C2 |

- Let's go through this example
- 


