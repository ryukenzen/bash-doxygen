bash-doxygen
============

A basic doxygen filter (originaly written in GNU sed) allowing you to
add inline-documentation to your bash shell scripts.

### Supported shell syntaxes

* All lines starting with a `## ` (without any leading blanks) are
  provided to doxygen. You can use all doxygen command you want in
  those lines. (see [doxygen
  documentation](http://www.stack.nl/~dimitri/doxygen/manual/commands.html)).

* Some top level declarations will be recognized if you use the
  `declare` primitive: 
  * `declare -a` for arrays
  * `declare -A` for associative arrays
  * `declare -i` for integers
  * Any other top-level `declare` statement will consider variable is a string.
  * Those additionnal declaration attributes can be combined with -A/-a/-i/<none>:
    * `declare -l` will mark the variable as LowerCase
    * `declare -u` will mark the variable as UpperCase
    * `declare -x` will mark the variable as Exported
    * `declare -r` will mark the variable as ReadOnly

* Functions declaration will be recognized if all these conditions are met:
  1. a `## @fn` line is found above the function declaration,
  2. the function is declared **without** the non-posix `function` keyword,
  3. the body-opening `{` char is on the same line than the
  `funcname()` instruction.

How to use it
-------------

1. If you do not have a Doxygen configuration file (usually named Doxyfile), you can generate one by simply running `doxygen -g`.
2. Edit the Doxyfile to map shell files to C parser: `EXTENSION_MAPPING = sh=C`
3. Set your shell script file names pattern as Doxygen inputs, like e.g.: `FILE_PATTERNS = *.sh`
4. Mention doxygen-bash.sed in either the `INTPUT_FILTER` or the
`FILTER_PATTERN` directive of your Doxyfile. If doxygen-bash.sed is in
your $PATH, then you can just invoke it as is, else use `sed -n -f
/path/to/doxygen-bash.sed --`.

Known limitations
-----------------

Yes.

FAQ
---

Q. Does it actually work ?  
A. The [bash-argsparse](https://github.com/Anvil/bash-argsparse)
project uses this filter. Check
[the result](http://argsparse.livna.org/doxygen/). Click on the
links. See by yourself.

Q. Is it rock-solid ?  
A. No.

Q. Do you accept patches ?  
A. Definitely.

Q. Why is the project named bash-doxygen while the filter is named
doxygen-bash ?  
A. Yeah, haha. Seriously.

Q. Can i include the doxygen-bash.sed file in my own tarball ?  
A. See the COPYING file.

Q. Dude. sed ? Seriously ?  
A. Are you.. Jealous ?

Q. ... ?  
A. Don't you dare !
