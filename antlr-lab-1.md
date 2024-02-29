## Harsh Vardhan Singh Chauhan
## 2022BCD0044

### 1. Arithmetic operation
```g
grammar Expr;
start: (expr NEWLINE)* ;
expr: expr ('*'|'/') expr
 | expr ('+'|'-') expr
 | INT
 | '(' expr ')'
 ;
NEWLINE : [\r\n]+ ;
INT : [0-9]+ ;
```
![antlr4_parse_tree](https://github.com/Harshtherocking/Compiler-Design-ICS-223/assets/65885345/43c0f6ca-86a8-4391-a1f4-3c3446877b51)

### 2. Boolean operation
```g
grammar BoolParser;
start : (boolexpr)* ;
boolexpr :
  boolexpr operator boolexpr
  | NOT boolexpr
  | '(' boolexpr ')' 
  | Variable
  ;
operator : AND | OR | EQUAL | LT | GT | LTE | GTE | NE ; 
NOT : '!';
AND : '&';
OR : '|' ;
EQUAL : '==' ;
LT : '<';
GT : '>';
LTE : '<=';
GTE : '>=';
NE : '!=';
Variable : [a-zA-Z0-9]+ ; 
SPACE : [ \t\r\n]+ -> skip;
```
![antlr4_parse_tree](https://github.com/Harshtherocking/Compiler-Design-ICS-223/assets/65885345/eb529268-7d56-492c-b872-a4ae4dfab10f)

### 3. If Else While loop 
```g
grammar IfElse;
start : code_block EOF;
code_block : statements;
statements : (line | if_stat | while_stat)*;
while_stat : WHILE condition conditional_block;
if_stat : IF condition conditional_block (ELSE IF condition conditional_block )* (ELSE conditional_block)?;
conditional_block : OFLOWER code_block CFLOWER;
condition : OPAREN bool_expr CPAREN;
bool_expr : OPAREN bool_expr CPAREN
          | NOT bool_expr
          | bool_expr (AND | OR | XOR | GT | GTE | LT | LTE | EQ | NEQ) bool_expr
          | (IDEN | INT | FLOAT | BOOl)
          ;
line : (((VAR_TYPE)? IDEN ASSIGN ( INT | FLOAT | IDEN | BOOl))? SEMICOLON)+;

arithmetic_expr : OPAREN arithmetic_expr CPAREN
                | arithmetic_expr (PLUS | MINUS | MULT | DIV) arithmetic_expr
                | (IDEN | INT | FLOAT )
                ;
IF        : 'if';
ELSE      : 'else';
WHILE     : 'while';
VAR_TYPE  : ( 'int' | 'float' | 'bool' );
IDEN      : [a-zA-Z_][a-zA-Z_0-9]*;
BOOl      : ( 'true' | 'false' );
INT       : [0-9]+;
FLOAT     : [0-9]+ '.' [0-9]*
          | '.' [0-9]+
          ;
OPAREN    : '(';
CPAREN    : ')';
OFLOWER   : '{';
CFLOWER   : '}';
NOT       : '~';
AND       : '&';
OR        : '|';
XOR       : '^';
GT        : '>';
GTE       : '>=';
LT        : '<';
LTE       : '<=';
EQ        : '==';
NEQ       : '!=';
ASSIGN    : '=';
SEMICOLON : ';';
PLUS : '+';
MINUS : '-';
MULT : '*';
DIV : '/';
SPACE     : [ \n\t\r] -> skip;
```
![antlr4_parse_tree](https://github.com/Harshtherocking/Compiler-Design-ICS-223/assets/65885345/f3376efe-9157-4ff2-986a-ca174d8c7105)
