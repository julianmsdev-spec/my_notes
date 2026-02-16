## What is Brainfuck?
Brainfuck has only eight commands `+ - . , > < [ ]`. 

## What makes a language turing-complete?
A programming language is considered Turing-complete if it can simulate a Turing machine, an abstract model of a machine that can implement any computer algorithm. 

## How Brainfuck works
The main state in a Brainfuck program is an array of integers. Each of the slots in the array is called a cell. 

## The Structure of an Interpreter
- A *tokenizer* (sometimes known as a *lexer*) that takes the original source code and divides it into the smallest recognizable constructs allowed in the programming language. These are known as *tokens*. For the code a + 2, the tokens may be a, +, and 2.
- A *parser* that takes tokens that are next to each other and figures out their meaning (that is, the expressions or statements they form). Parsers typically produce a tree of nodes representing the relative relationships between expressions, statements, and literal values. This tree is called the *abstract syntax tree (AST)*. For example, if a Python interpreter saw the token a followed by the token + followed by the token 2, it may construct an arithmetic expression node and connect it to nodes for the a and the 2.
- A *runtime environment* that walks through the nodes of the AST and runs the appropriate operations to execute the meaning inherent in them. For our a + 2 arithmetic expression node, this would mean looking up the value represented by a and adding 2 to it.