# Harsh Vardhan Singh Chauhan
### 2022BCD0044

1.
```l
%{

#include<stdio.h>
#include"main.tab.h"
extern int yylval;

%}

%%

[a-zA-Z][a-zA-Z0-9]* {return ID;}
[\t] {return yytext[0];}
[\n] {return 0;}
[ ] {return 0;}

%%

int yywrap()
{ 
return 1;
}
```
```y
%{
#include<stdio.h>
#include<stdlib.h>
int yylex();
void yyerror();
%}

%token ID

%%

start:  E '\n'
     ;

E:  ID           { printf("ID\n"); }
 |  E '+' E
 |  E '-' E
 | '(' E ')'
 ;

%%
```

2.
```l
%{

#include<stdio.h>
#include"main.tab.h"
extern int yylval;

%}

%%

[a-zA-Z][a-zA-Z0-9]* {return ID;}

%%

int yywrap()
{ 
return 1;
}
```
```y
%{
#include<stdio.h>
#include<stdlib.h>
int yylex();
void yyerror();
%}

%token ID

%%

start:  ID '\n'
     ;

%%
```
