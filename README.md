# Toy-Language-Interpreter
Toy Language Interpreter application, 3rd semester.

# Toy Language Description
A program (Prg) in this language consists of a statement (Stmt) as follows:

Prg := Stmt where the symbol "::=" means "a Prg is defined as a Stmt".

A statement can be either a compound statement (CompStmt), or an assignment statement

(AssignStmt), or a print statement (PrintStmt), or a conditional statement (IfStmt) as follows:
```
Stmt ::= Stmt1 ; Stmt2 /* (CompStmt)*/

| Type Id /* (VarDecl) */
  
| Id = Exp /* (AssignStmt)*/
  
| Print(Exp) /* (PrintStmt)*/
 
| If Expr Then Stmt1 Else Stmt2 /* (IfStmt)*/
  
| nop /* No operation */
```
where the symbol "|" denotes the possible definition alternatives.

A type Type can be :
```
Type ::= int

  | bool
 ```
A value Value in our language can be either an integer number (ConstNumber), or boolean values like (ConstTrue) or (ConstFalse):
```
Value ::= Number /*(ConstNumber)*/

  | True /* (ConstTrue)*/

  | False /* (ConstFalse)*/
```
An expression (Exp) can be either a value (Value), or a variable name (Var), or an arithmetic expression (ArithExp), or a logical expression (LogicExp), as follows:
```
Exp ::= Value /*Value*/

  | Id /*(Var)*/

  | Exp1 + Exp2 /*(ArithExp)*/

  | Exp1 - Exp2

  | Exp1 * Exp2

  | Exp1 / Exp2

  | Exp1 and Exp2 /*(LogicExp)*/

  | Exp1 or Exp2
```
Example1:
```
  int v;

  v=2;

  Print(v)
```
Example2:
```
  int a;

  a=2+3*5;

  int b;

  b=a-4/2 + 7;

  Print(b)
```
Example3:
```
  bool a;

  a=false;

  int v;

  If a Then v=2 Else v=3;

  Print(v)
```
Toy Language Evaluation (Execution):

Our mini interpreter uses three main structures:

	– Execution Stack (ExeStack): a stack of statements to execute the currrent program

	– Table of Symbols (SymTable): a table which keeps the variables values

	– Output (Out): that keeps all the mesages printed by the toy program

All these three main structures denote the program state (PrgState). Our interpreter can execute multiple programs but for each of them use a different PrgState structures (that means different ExeStack, SymTable and Out structures). 

At the beginning, ExeStack contains the original program, and SymTable and Out are empty. After the evaluation has started, ExeStack contains the remaining part of the program that must be evaluated, SymTable contains the variables (from the variable declarations statements evaluated so far) with their assigned values, and Out contains the values printed so far.

In order to explain the program evaluation rules, we represent ExeStack as a collection of statements separated by the symbol "|", SymTable as a collection of mappings and Out as a collection of messages.
For example, the ExeStack {s1 | s2 | s3} denotes a stack that has the statement s1 on top of it, followed by the statement s2 and at the bottom of the stack is the statement s3.
For example, SymTable {v->2,a->false} denotes the table containing only two variables v and a, v has assigned the integer value 2, while a has assigned the boolean value flase.
For example Out {1,2} denotes the printed values, the order of printing is 1 followed by 2.

At the end of a program evaluation, ExeStack is empty, SymTable contains all the program variables, and Out contains all the program print outputs.

Statement Evaluation Rules: are described by presenting the program state (ExeStack1,SymTable1,Out1) before applying the evaluation rule, the symbol "==>" for one step evaluation and the program state (ExeStack2,SymTable2,Out2) after applying the evaluation rule. Each evaluation rules shows how the program state is changed. One step evaluation means that only one statement evaluation rule is applied. Complete evaluation means that all possible evaluation rules are applied until the program evaluation terminates. Termination means that there is no any evaluation rule that can be further applied.
