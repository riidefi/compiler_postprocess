# compiler_postprocess
Patches supporting decompilation with the CodeWarrior compiler.

## Usage
`postprocess.py [args] file`


This script is the culmination of three patches supporting decompilation with the CodeWarrior compiler.

1) Certain versions have a bug where the ctor alignment is ignored and set incorrectly.
   This option is enabled with `-fctor-realign`, and disabled by default with `-fno-ctor-realign`

2) Certain C++ symbols cannot be assembled normally.
   To support the buildsystem, a simple substitution system has been devised

   ?<ID> -> CHAR

   IDs (all irregular symbols in mangled names):
      0: <
      1: >
      2: @
      3: \\
      4: ,
      5: -

   This option is enabled with `-fsymbol-fixup`, and disabled by default with `-fno-symbol-fixup`

3) CodeWarrior versions below 2.3 used a different scheduler model.
   The script can currently adjust function epilogues with the `old_stack` option.
   `-fprologue-fixup=`[default=`none`, `none`, `old_stack`]
