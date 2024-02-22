# Harsh Vardhan Singh Chauhan (2022BCD0044)
## Downloading ANTLR
```console
sudo apt install antlr4
```
```console
sudo curl -O https://www.antlr.org/download/antlr-4.8-complete.jar
```
## Downloading JDK
```console
sudo apt install openjdk-21-jdk
```
## Creating `Expr.g`
```g
grammar Expr;
start: (expr NEWLINE)* ;
expr: expr ('*'|'/') expr
	| expr ('+'|'-') expr 
	| INT 
	| '(' expr ')' ; 
NEWLINE : [\r\n]+ ;
INT : [0-9]+ ;
```
## Creating `Sample` 
```
100+22*44
```
## Compilation
```console
export CLASSPATH="/usr/share/java/antlr-4.8-complete.jar:$CLASSPATH"
``` 
``` console
antlr4 Expr.g
```
```console
javac Expr*.java
```
```console
java org.antlr.v4.gui.TestRig Expr start ./Sample -gui
```
## Output 
![antlr4_parse_tree](https://github.com/Harshtherocking/Compiler-Design-ICS-223/assets/65885345/836079b2-be8b-4c1a-84b4-ab67c65083cb)
