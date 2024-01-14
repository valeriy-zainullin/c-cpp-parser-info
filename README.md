# c-cpp-parser-info

Collection (of handpicked) resources regarding c and c++ parsing

1. You may need to store identifier types while parsing to disambiguate the grammar.

    Links:
    1. https://eli.thegreenplace.net/2012/07/05/how-clang-handles-the-type-variable-name-ambiguity-of-cc (what clang does, lexer sometimes put the right identifier kind in other cases)

    For example, it's needed for c99. I've seen the problem myself..
    ```c
      void func()
         A * B;
      }
    ```
    This can be both a declaration and an expression. In pascal all declarations are annotated and reside at the start of a function. That disambiguates declarations and expressions in function body (although, maybe it's not convinient sometimes..)

    Usually the parser forwards information back to the lexer, so that lexer produces the right identifier kinds (type name, function name, variable name or etc..). (Link 1) clang has token streams and injects identifier info into the token stream, the token type is not just identifier, but typename or etc, when token is retried (first time it's a general type identifier, parser queries scope stack).

    With these hacks involved parser may not be pure like LR(1). But it's still a small modification, it may be pure with the assumption that identifiers are disambiguated (I haven't finished implementing the parser at the moment, so I don't know for sure).

1. You may need a custom parser for C++ or a GLR parser perhaps (infinite lookahed may be required). Bison can do GLR.

    Links:
    1. https://stackoverflow.com/a/243447 (discussion about c++ grammar, link to ultimate lambda thread)
    1. http://lambda-the-ultimate.org/node/2158#comment-27800 (ultimate lambda thread, some experience from people, link to fog PhD thesis)
    1. http://web.archive.org/web/20190303162600/http://www.computing.surrey.ac.uk/research/dsrg/fog/FogThesis.pdf (Fog PhD thesis, quite detailed overview from the first glance I was able to get)
