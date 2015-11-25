
# The Jeden Language

## Language Specification
*This section is normative*

### Grammar

The `teaser` release of the Jeden interpreter parses the following grammar.

```
    module      ::= defblock*
    defblock    ::= decl def
    decl        ::= context? ':-' ident ':' type
    def         ::= typclause* | trmclause*

    trmclause   ::= clhead cltail
    clhead      ::= (pat+ '>=')? ident '=>' pat+
    cltail      ::= action*
    action      ::= (pat+ '>-')? ident ('->' pat+)?

    typclause   ::= (typlist '>:')? ident ':>' type
    typlist     ::= ( type | '(' type ')' )+

    context     ::= ctxelem (',' ctxelem)*
    ctxelem     ::= var ':' type

    # priorities [associativity]:
    #   type type [left]
    #   type -> type [right]
    #   type * type [right]
    typeexpr    ::= typeprod
    typeprod    ::= typefun ('*' typeprod)*
    typefun     ::= typeapp ('->' typefun)*
    typeapp     ::= typeatom (typeatom typeatom*)?
    typeatom    ::= 'Type' | ident | '(' typeexpr ')'

    var         ::= ident
    pat         ::= ident | '(' pat* ')'
    ident       ::= alphanum+
```
