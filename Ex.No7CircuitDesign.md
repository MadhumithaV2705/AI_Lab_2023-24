# Ex.No: 7  Logic Programming –  Logic Circuit Design
### DATE:                                                                            
### REGISTER NUMBER : 
### AIM: 
To write a logic program to design a circuit like half adder and half subtractor.
###  Algorithm:
1. Start the Program
2. Design a AND gate logic if both inputs are 1 then output is 1.
3. Design a OR gate logic if any one of input is 1 then output is 1.
4. Design a XOR gate logic if both inputs are different then output is 1.
5. Design a NOT gate logic if input is 0 then output is 1.
6. Design a half adder and half subtractor using the rules.
7. Test the logic.
8. Stop the program.

### Program:
```
xor(0,0,0).
xor(0,1,1).
xor(1,0,1).
xor(1,1,1).
and(0,0,0).
and(0,1,0).
and(1,0,1).
and(1,1,1).
not(0,1).
not(1,0).
or(0,1,1).
or(1,0,1).
or(0,0,0).
or(1,1,1).
halfadder(X,Y,S,C):-
    xor(X,Y,S),
    and(X,Y,C).
halfsubtractor(X,Y,Sub,B):-
    xor(X,Y,Sub),
    not(X,Z),
    and(X,Y,B).
fulladder(X,Y,Z,S,C):-
    xor(X,Y,T1),
    and(X,Y,T2),
    and(T1,Z,T3),
    xor(T1,Z,S),
    or(T2,T3,C).
```
### Output:
<img width="944" height="336" alt="image" src="https://github.com/user-attachments/assets/e88d06ea-728c-43e9-8869-68761671c3d3" />
<img width="947" height="357" alt="image" src="https://github.com/user-attachments/assets/66e3e39d-9570-439c-9e81-50f530579291" />
<img width="940" height="356" alt="image" src="https://github.com/user-attachments/assets/342e6742-a035-4ee1-b117-92cc9626fa5c" />

### Result:
Thus the truth table of circuit verified sucessfully.
