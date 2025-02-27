```ebnf
document       ::= { block } ;

block          ::= code_block | markdown_block ;

code_block     ::= s_expr newline { s_expr newline }*
  (* Any well-formed S‑expression at the beginning of a line is a code block *)

markdown_block ::= { markdown_line newline }+
  (* Lines not starting with a valid S‑expression are treated as plain markdown *)

markdown_line  ::= { inline } ;
inline         ::= text | interpolation ;
text           ::= ( any characters except the substring "{{" ) ;
interpolation  ::= "{{" s_expr "}}" ;
  (* Interpolates a reactive expression into markdown *)

s_expr         ::= "(" { s_expr | atom } ")" ;
atom           ::= identifier | number | string | keyword ;
identifier     ::= letter { letter | digit | "-" | "/" } ;
number         ::= digit { digit } ;
string         ::= "\"" { character } "\"" ;
keyword        ::= ":" identifier ;

newline        ::= "\n" ;
```