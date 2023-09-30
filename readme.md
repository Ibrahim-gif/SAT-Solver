# SAT Solver
A SAT solver is an algorithm for establishing satisfiability. It takes the Boolean logic formula as input and returns if it finds a combination of variables that can satisfy it or if it can demonstrate that no such combination exists.

Context-free Grammar for Valid Inputs
One valid input shall be a string generated from the Context-Free Grammar G below:

```
S ::= Formula ’;’ Assignments
Formula ::= ConjTerm | ConjTerm ’+’ Formula
ConjTerm ::= Term | Term ’*’ ConjTerm
Term ::= Constant | VarName | ’-’Term | ’(’ Formula ’)’
Assignments ::= an empty string | Assignment | Assignment ’,’ Assignments
Assignment ::= VarName ’:’ Constant
VarName ::= a continuous sequence of letter (upper- or lowercase) or digits (0-9);
the first character cannot be a digit; the total length shall be no longer than 10
Constant ::= ’0’ | ’1’
```

# Semantics of the Input
One valid input consists of a string representation of a Boolean formula SF and a string representation of an
assignment SA, separated by a semicolon.
In SF , ”1” and ”0” represent Boolean constants TRUE and FALSE, respectively; a Boolean variable is a
sequence of letters (either in upper- or lowercase) or digits (0-9); however, the variable name cannot start with a
digit and its total length cannot be longer than 10. ”+” represents the 2-argument infix Boolean function OR; ”∗”
represents the 2-argument infix Boolean function AND; ”−” represents the prefix 1-argument Boolean function
NOT. The order of operations is: parenthesis > NOT > AND > OR.


# Sample Run
The executable shall be called pa1 present in Tokenizing and Parsing dir
```
$ ./pa1
1 * VAr ; VAr: 1, VAr: 0
Error: contradicting assignment
1
1 * VAr;VAr : 0
0
Error: invalid input
(1 * (a1 +VAr)) ; VAr: 1, a1: 0, VAr: 0
Error: contradicting assignment
1 *(VAr + 0 );
Error: incomplete assignment
```

# Transformation and Satisfibility 
Transform a Boolean formula F into an equivalent CNF formula F' using Tseitin's Transformation. The program parses a formula string input using the PA1 formula parser and outputs the satisfiability result of F using a SAT solver on F'.

The program continuously accepts input from standard input and provides output to standard output. In case of errors, error messages will be displayed on standard output, starting with "Error:" followed by a brief description. The program gracefully terminates upon encountering the end of the input (EOF) and does not generate any unnecessary prompts or additional output.

# Sample Run
Sample Run
The executable shall be called pa2 present in Transformation and Satisfiability dir
```
$ ./pa2
a123
sat
a+c
sat
a* -- -a
unsat
(( -a)+(a*b)) *
Error: invalid input
(1+2+3)*(1+2+ -3)*(1+ -2 +3)*-1
Error: invalid input
```