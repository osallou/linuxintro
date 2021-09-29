# Environment variables

It is possible to use variables within a terminal or script.

*warning* Variables are case sensitive.

To define a variable:

    MYVARIABLE=1234

*warning* There should be no whitespace before or after the equal sign.

Usually variables are uppercased, but this is not mandatory.

Then variable can be used later using its name, prefixed with a dollar sign "$"

    $ echo "hello $MYVARIABLE"

It is also possible to use ${MYVARIABLE}

A variable is visible only in the scope of the current session, so it cannot be shared between different
opened sessions (multiple terminals).

If a script is called, variable won't be visible inside the script.
To make the variable available to a sub-process, it needs to be exported

    $ MYVARIABLE=123
    $ ./test.sh  # $MYVARIABLE **cannot** be used in test.sh

    $ export MYVARIABLE=123
    $ ./test.sh  # $MYVARIABLE can be used in test.sh

To avoid export and use an environment variable in a subprocess on a per call basis,
simply add its definition on the same command line

    $ MYVARIABLE=123 ./test.sh

Variables can also contain the result of an other command using back ticks

    MYVARIABLE=`date`
    echo $MYVARIABLE