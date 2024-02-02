## Harsh Vardhan Singh Chauhan
## 2022BCD0044
### 1. IIIT Kottayam 
```c
{
#include <stdio.h>
%}
id (20)((1[89])|(2[0-3]))((BC[SDY])|(BEC))([0][0-9]{3})
%%
{id} {
if (yytext[yyleng-1]=='0' && yytext[yyleng-2]=='0' && yytext[yyleng-3]=='0') {
printf("Invalid");
} else {
printf("Valid");
}
}
%%
int yywrap() {return 1;}
int main() {yylex();}
```


### 2. Valid phone number 
```c
%{
#include<stdio.h>
FILE *f;
%}
num (\+(91)|0)?[ ]* ?[6-9][0-9]{9}

%%
num {printf("Valid");}
.* {printf("Not Valid");}
%%

int yywrap()
{
 return 1;
}

int main(int argc,char *argv[])
{
 f=fopen(argv[1],"r");
 yyin=f;
 yylex();
 return 0;
}
```

