[![Actions Status](https://github.com/tbrowder/Getopt-Easy/actions/workflows/linux.yml/badge.svg)](https://github.com/tbrowder/Getopt-Easy/actions) [![Actions Status](https://github.com/tbrowder/Getopt-Easy/actions/workflows/macos.yml/badge.svg)](https://github.com/tbrowder/Getopt-Easy/actions) [![Actions Status](https://github.com/tbrowder/Getopt-Easy/actions/workflows/windows.yml/badge.svg)](https://github.com/tbrowder/Getopt-Easy/actions)

NAME
====

**Getopt::Easy** - Provides easy generation of CLI modes, options, and short and long help

SYNOPSIS
========

```raku
use Getopt::Easy;
# produce a specially formatted source file
# run the included binary:
$ gen-easy <input file>
...
See output files:
lib/MyModule/Action.rakumod
bin/myaction
...
```

DESCRIPTION
===========

**Getopt::Easy** is an easy way to handle simple input arguments as well as the required supporting files. Given the single input file, the CLI binary is created along with CLI short and long help, a subroutine call for each mode (inluding its options), a Rakumod file with those subroutines and signatures in place, and a README.rakudoc fragment to add to an existing README.rakudoc.

In sum, you can use a single source file to ensure your README and help output stay current for your public module.

A simple example
----------------

  * The source file

    mode: abc             # comments are ignored
                          # this blank line is ignored
    a short help line     # the first non-empty line is short help
    a longer text section # the rest is long help, paras are indicated
    till the next def     # by blank lines

    option: -f # options and modes can have one or more leading hyphens
    short help # which are ignored for now

    mode: def # 
    some help

Modes and options are collected into a separate hash for each mode and option set. Each set is assigned to a handler sub named `` with signature ``.

  * The generated CLI bin file

    use Actions;
    #!/usr/bin/env raku
    if not @*ARGS { action }
    else { action @*ARGS }

  * The generated Rakumod file

    unit module Actions;
    sub action {

    }
    sub action(@args) {
    }

  * The generated Rakudoc fragment

AUTHOR
======

Tom Browder <tbrowder@acm.org>

COPYRIGHT AND LICENSE
=====================

© 2024 Tom Browder

This library is free software; you may redistribute it or modify it under the Artistic License 2.0.

