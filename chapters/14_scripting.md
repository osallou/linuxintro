# Bash scripting

A Bash script allows us to define a series of actions which the computer will then
perform without us having to enter the commands ourselves.
If a particular task is done often, or it is repetetive, then a script can be a useful tool.

A Bash script is interpreted (read and acted upon) by something called an interpreter.
There are various interpreters on a typical linux system but we have been learning the
Bash shell so we'll introduce bash scripts here.

A script is a text file, usually with extension .sh with executable rights

    $ touch test.sh
    $ chmod +x test.sh

Now let's edit a simple script


    #!/bin/bash
    ls -l
    echo "hello"

The first line is what is called shebang. It gives the path to the interpreter.
Then each line gives a shell command to execute (like you would via the command-line).

A script accepts arguments. In the script they can be refered by $1, $2, etc.

To get the list of all input arguments, you can use $@

Example, update script test.sh:

    #!/bin/bash
    echo "arg1: $1"
    echo "all args: $@"

Then execute:

    # ./test.sh myarg1 myarg2  (or bash test.sh)
    arg1: myarg1
    all args: myarg1 myarg2