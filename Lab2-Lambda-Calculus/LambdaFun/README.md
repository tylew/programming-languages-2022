```
  $$$$\        $$$$$$$$\                     
    $$ \       $$  _____|                    
     $$ \      $$ |    $$\   $$\ $$$$$$$\  
     $$$ \     $$$$$\  $$ |  $$ |$$  __$$\ 
    $$ $$ \    $$  __| $$ |  $$ |$$ |  $$ |
   $$ / $$ \   $$ |    $$ |  $$ |$$ |  $$ |
 $$$ /   $$$\  $$ |    \$$$$$$  |$$ |  $$ |
 \___|   \___| \__|     \______/ \__|  \__|
```

To compile run `stack build` and to launch the REPL, run `stack exec lamfun`. For help, type `:help` in the REPL...

The full grammar of λFun is given below:

```
<statement> ::= <expr> ";;" | <defn> ";;"
<defn>      ::= "val" <id> "=" <expr> | "rec" <id> " " <ids> "=" <expr>
<expr>      ::= <id> | 
                <number> | 
                "true" | 
                "false" | 
                "\" <ids> "." <expr> | 
                <expr> " " <expr> | 
                <expr> <op> <expr> | 
                "[" <list> "]" | 
                <expr> ":" <expr> |
                "let " <defn> " in " <expr> | 
                "case " <expr> " of " "{" <case> "}" |
                "while " <expr> " do " <expr> | 
                <expr> ";" <expr> |
                <expr> ":=" <expr> | 
                "!" <expr> | 
<list>      ::= "" | <expr> "," <list>
<expr_opt>  ::= "_" | <expr>
<case>      ::= <expr_opt> "->" <expr> | <expr_opt> "->" <expr> "," <case>
<id>        ::= <letter> | <id> <letter> | <id> <digit>
<ids>       ::= <id> | <id> " " <ids>
<op>        ::=  "*" | "+" | "-" | "/" | ">" | ">=" | "==" | "!=" | "=<" | "<"
<number>    ::= <digit>+
<string>    ::= """ (<letter>|<digit>)* """
```

Remark: 

- `while a do b ; c` is parsed as `(while a do b) ; c`, not as `while a do (b ; c)`
- Use `:tree` if you want to see the abstract syntax tree.
- There are built-in functions defined in all environments as follows.

  - One for each `<op>`.
  - A function `new` to allocate memory.
  - Functions `head` and `tail` to take the head or tail of a list.
  - A function `addr` that converts a value (number) into an address.

## Lab2

See `test/examples.lc` for examples to get started.
