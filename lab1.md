# Lab - 1
### Harsh 2022BCD0044
### 1. Write a lex program to count number of vowels and consonants 
```lex
%{
#include<stdio.h>
int cons = 0;
int vowels= 0;    
%}

%%
[aeiouAEIOU] {vowels++;}
[a-zA-Z] {cons++;}

%%
//[\t\n]+ ;
//[^aeiouAEIOU] {cons++}
int yywrap()
{
    return 1;
}

int main()
{
    printf("Enter the string.. at end press ^d\n");
    yylex();
    printf("No of vowels=%d\nNo of consonants=%d\n",vowels,cons);
}
```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex vowels.l
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c -o vowel.exe
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./vowel    
Enter the string.. at end press ^d
abcdefghi
^Z  
No of vowels=3
No of consonants=6
```

### 2. Write lex program to print number and string from the given sequence
```lex
%{
#include<stdio.h>
int cons = 0;
int vowels= 0;    
%}

%%
[aeiouAEIOU] {vowels++;}
[a-zA-Z] {cons++;}

%%
//[\t\n]+ ;
//[^aeiouAEIOU] {cons++}
int yywrap()
{
    return 1;
}

int main()
{
    printf("Enter the string.. at end press ^d\n");
    yylex();
    printf("No of vowels=%d\nNo of consonants=%d\n",vowels,cons);
}
```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a 
Enter the string.. at end press ^d
Harsh12345
 strings: Harsh
 numbers: 12345
```
### 3. Write a lex program to Identify Numbers
```lex
%{
#include<stdio.h>
FILE *f;
%}
Binary [0-1]+
oct [0-7]+
dec [0-9]+
hex [0-9A-F]+
Float [-+]?[0-9]*\.?[0-9]+
exponent [-+]?[0-9]*\.[0-9]+([eE][-+]?[0-9]+)?
%%
{Binary} {printf("%s is a binary number\n",yytext);}
{oct} {printf("%s is an octal number\n",yytext);}
{dec} {printf("%s is a decimal number\n",yytext);}
{hex} {printf("%s is a hexadecimal number\n",yytext);}
{Float} {printf("%s is a float number\n",yytext);}
{exponent} {printf("%s is an exponent number\n",yytext);}
%%
int yywrap()
{
    return 1;
}
int main(int argc,char *argv[])
{
    //printf("Enter the string:")
    f=fopen(argv[1],"r");
    yyin=f;
    yylex();
    return 0;
}
```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex q3.l   
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a         
1
1 is a binary number

0101
0101 is a binary number

2
2 is an octal number

229
229 is a decimal number

393.309
393.309 is a float number

afaf64
afaf64 is an octal number

afaf23
afaf23 is an octal number

22.1e3
22.1e3 is an exponent number
```
### 4. Write a lex program to find count of number of positive and negative integers and fractions
```lex
%{
#include<stdio.h>
int cp=0;
int cn=0;
int fp=0;
int fn=0;
%}
pos \+?[0-9]+
neg -[0-9]+
frap (\+?)[0-9]*\.[0-9]+
fran (\-?)[0-9]*\.[0-9]+
%%
{pos} {cp++;printf("%s is positive integer\n",yytext);}
{neg} {cn++;printf("%s is a negative integer\n",yytext);}
{frap} {fp++;printf("%s is a positive fractional number\n",yytext);}
{fran} {fn++;printf("%s is a negative fractional number\n",yytext);}
%%
int yywrap()
{
    return 1;
}
int main()
{
    printf("Enter numbers:");
    yylex();
    printf("Number of positive integers:%d\n Number of negative integers:%d\n Number of positive 
fractions:%d\n Number of negative fractions:%d\n",cp,cn,fp,fn);
}
```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex q3.l   
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a
Enter numbers:1
1 is positive integer

2
2 is positive integer

011101
011101 is positive integer

.23
.23 is a positive fractional number

-12
-12 is a negative integer

Number of positive integers:3
 Number of negative integers:1
 Number of positive fractions:1
 Number of negative fractions:0
```

### 5. Write a Lex Program to recognize and display keywords, numbers, and words in a given statement
```lex
 %{
#include<stdio.h>
%}
key if|else|while|do|int|float|char
spec ,|;
num [0-9]+
word [a-zA-Z]+
%%
{key} {printf("%s is a keyword\n",yytext);}
{num} {printf("%s is a number\n",yytext);}
{word} {printf("%s is a word\n",yytext);}
{spec} {printf("%s is a special character\n",yytext);}
%%
int yywrap()
{
    return 1;
}
int main()
{
    printf("Enter the statement:");
    yylex();
    return 0;
}

```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex q5.l   
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a
Enter the statement:Harsh
Harsh is a word

234
234 is a number

l;asjdf
l is a word
; is a special character
asjdf is a word

hahrs
hahrs is a word

2345
2345 is a number
```
### 6. Lex program to identify the capital words from the given input string
```lex
%{
#include<stdio.h>
int c=0;
%}
noncapital [\n\t]*[a-z]+[A-Z]*[\n\t]*
capital [A-Z]+[a-z]*
%%
{noncapital} {printf("\n");}
{capital} {c++;printf("%s is a capital word\n",yytext);}
%%
int yywrap()
{
return 1;
}
int main()
{
    printf("Enter the string:");
    yylex();
    printf("Number of capital words:%d\n",c);
    return 0;
}
```
```console
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex q6.l   
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a         
Enter the string:Harsh
Harsh is a capital word
harsh
Hellp

Hellp is a capital word
```

### 7. How to write Lex Program to recognize given statement is Simple or Compound
```lex
%{
#include<stdio.h>
int c=0;
%}
%%
if|else|while|do|and|but|then {c=1;}
. ;
\n {return 0;}
%%
int yywrap()
{
    return 1;
}
int main()
{
    printf("Enter the statement:\n");
    yylex();
    if(c==0)
    printf("Simple sentence");
    else
    printf("Compound sentence");
    return 0;
}
```
```console

PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> flex q7.l   
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> gcc lex.yy.c
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a         
Enter the statement:
Harsh is happy and sa
Compound sentence
PS C:\Users\harsh\OneDrive\Desktop\Compiler Course> ./a
Enter the statement:
Harsh is happy
Simple sentence
```
