# The command line

## where it starts...

When starting a *terminal* (locally or via remote connection), several things
happen behind the scenes.

System preload some scripts (usually /etc/profile (for all users) and $HOME/.bashrc
(your own, editable, setting file) (if using bash as default shell).
Those scripts sets set default variables and environment.

Then user gets a *prompt* in his home directory, something like:

    userA@myserver $

This may vary a lot depending on system defaults or preload scripts (and can
be customized)

Once the prompt appears, one can use the command line....

It several shell windows/connections are opened, a new session starts (with preloads etc.),
and each session is independant.

## the terminal

Within a terminal you have what is known as a shell. This is a part of the operating system that defines how the terminal will behave and looks after running (or executing) commands for you. There are various shells available but the most common one is called bash which stands for Bourne again shell. This tutorial will assume you are using bash as your shell.

As said above, some environment variables are set by the set, and can be updated later one.
To get the list of available variables:

    $ env
    SHELL=/bin/bash
    HOME=/home/user
    TMPDIR=/tmp
    ...

Environment variables can be used with the "$" prefix

If you would like to know which shell you are using you may use a command called echo to display a system variable stating your current shell. echo is a command which is used to display messages.

    $ echo $SHELL
    /bin/bash

Important variable is *PATH*. It contains the list of directories will look for when calling a program.
If program directory is not in *PATH* then full path to the program needs to be used. If in *PATH*, one
can just use its name.

    $ echo $PATH
    /usr/bin:/bin:...

In above example, the echo binary is in /usr/bin, so echo is automatically found by the system.
If /usr/bin was not in the PATH, you should have called

     $ /usr/bin/echo $SHELL

