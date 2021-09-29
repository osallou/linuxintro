# Bash scripting

## Scripts

A Bash script allows us to define a series of sequential actions.
It helps to automate repetitive tasks or manage complex logic.

A Bash script is ran by something called an interpreter, a script is not compiled.

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

## Comments

Comments in a script a prefixed by "#"

    #!/bin/bash
    # this is my program
    echo hello

## Conditions

Among the different functions, it is possible to use if conditions

    TEST="aaa"
    if [ $TEST == "aaa" ]; then
        echo "good"
    else
        echo "bad"
    fi

    if [ -e "file1" ]; then
        echo "file1 exists
    fi

you should take care of spaces with brakets etc.. For more information on syntax, comparisons etc..
you will find good documentation on the net.

## Loops

Bash also manage loops using for, while, ...

    # The for will iterate over stuff defined after the  *in* and put value in environment variable *VARIABLE*
    # Then variable can be used with the $ prefix
    for VARIABLE in file1 file2 file3
    do
        echo "i should do something with $VARIABLE
    done

    # Iterate 5 times
    for i in {1..5}
    do
    echo "Welcome $i times"
    done

break can be used to exit the loop


## Read from file or stdin

Example script:

    #!/bin/bash

    # read line by line until end of file
    while read line
    do
    echo "$line"
    # ${1:-/dev/stdin} means redirect content of $1 (first argument), else if there is no argument, read from stdin
    done < "${1:-/dev/stdin}"

Execute with argument (read the script ifself for example, or an other one)

    $ bash /tmp/test.sh /tmp/test.sh 
    #!/bin/bash

    while read line
    do
    echo "$line"
    done < "${1:-/dev/stdin}"

Execute, forwarding file content to script stdin

    $ bash /tmp/test.sh < /tmp/test.sh 
    #!/bin/bash

    while read line
    do
    echo "$line"
    done < "${1:-/dev/stdin}"

Execute with no argument, instead use piping to forward
the ouput of previous command to the script input

    $ cat /tmp/test.sh | bash /tmp/test.sh
    #!/bin/bash

    while read line
    do
    echo "$line"
    done < "${1:-/dev/stdin}"

## Exit

To stop a program before it reaches the end, just call exit with an error code (0 for success)

    TEST="aaa"
    if [ $TEST == "aaa" ]; then
        echo "good"
    else
        exit 1
    fi
