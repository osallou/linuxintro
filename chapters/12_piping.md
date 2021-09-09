# Piping and redirections

## Data streams

Every program we run on the command line automatically has three data streams
connected to it.

* STDIN (0) - Standard input (data fed into the program)
* STDOUT (1) - Standard output (data printed by the program, defaults to the terminal)
* STDERR (2) - Standard error (for error messages, also defaults to the terminal)

Piping and redirection is the means by which we may connect these streams between
programs and files to direct data in interesting and useful ways.

We'll demonstrate piping and redirection below with several examples but these
mechanisms will work with every program on the command line,
not just the ones we have used in the examples.

# Redirecting to a File

Normally, we will get our output on the screen, which is convenient most of the time,
but sometimes we may wish to save it into a file to keep as a record,
feed into another system, or send to someone else.
The greater than operator ( > ) indicates to the command line that we wish the programs
output (or whatever it sends to STDOUT) to be saved in a file instead of printed to the
screen. Let's see an example.

    $ ls
    file1 file2
    $ ls > myoutput
    $ ls
    file1 file2 myoutput

Here we use the > to tell the terminal to save the output into the file myoutput.
You'll notice that we don't need to create the file before saving to it.
The terminal will create it automatically if it does not exist.

You'll notice that in the above example, the output saved in the file was one file per
line instead of all across one line when printed to the screen.
The reason for this is that the screen is a known width and the program can format its
output to suit that. When we are redirecting, it may be to a file, or it could be
somewhere else, so the safest option is to format it as one entry per line.
This also allows us to easier manipulate that data later on as we'll see further down
the page.

*warning*: If we redirect to a file which does not exist, it will be created
automatically for us.
If we save into a file which already exists, however, then it's contents will be
cleared, then the new output saved to it.

## redirecting from a file

To use the content of a file as input for a program we can use the "<" character.
It will forward content to the STDIN of the program

    $ wc -l myoutput
    8 myoutput
    $ wc -l < myoutput
    8


We may easily combine the two forms of redirection we have seen so far into a single
command as seen in the example below.

    $ wc -l < mysampledata.txt > myoutput
    $ cat myoutput
    12

We send mysampledata.txt content to wc STDIN and ask to redirect wc STDOUT to file
myoutput.

## Redirecting STDERR

Now let's look at the third stream which is Standard Error or STDERR.
The three streams actually have numbers associated with them
(in brackets in the list at the top of the page).
STDERR is stream number 2 and we may use these numbers to identify the streams.
If we place a number before the > operator then it will redirect that stream
(if we don't use a number, like we have been doing so far, then it defaults to stream 1).

    $ ls -l file1 blah.foo
    ls: cannot access blah.foo: No such file or directory
    rwxr-xr-x  2 user1 team1 4096 Mar 23 13:34 file1

    $ ls -l file1 blah.foo 2> errors.txt
    rwxr-xr-x  2 user1 team1 4096 Mar 23 13:34 file1
    $ cat errors.txt
    ls: cannot access blah.foo: No such file or directory


Maybe we wish to save both normal output and error messages into a single file.
This can be done by redirecting the STDERR stream to the STDOUT stream and redirecting
STDOUT to a file. We redirect to a file first then redirect the error stream.
We identify the redirection to a stream by placing an & in front of the stream number
(otherwise it would redirect to a file called 1).

    $ ls -l file1 blah.foo > myoutput 2>&1

## Piping
So far we've dealt with sending data to and from files.
Now we'll take a look at a mechanism for sending data from one program to another.
It's called piping and the operator we use is ( | )
(found above the backslash ( \ ) key on most keyboards).

What this operator does is feed the output from the program on the left
as input to the program on the right.
In the example below we will list only the first 3 files in the directory.

    $ ls
    file1 file2 file3 dir1
    ls | head -3
    file1
    file2
    file3

We may pipe as many programs together as we like.
In the below example we have then piped the output to tail so as to get
only the third file.

    $ ls | head -3 | tail -1
    file3

Using *xargs* we can pipe the result of command to use them as arguments to the next command

    # let's first add some content to files
    $ echo "aaaaa" > file1
    $ echo "bbbbb" > file2
    $ find . -type f | xargs grep aa  # find all files, and for each match, apply a filter on file content
    ./file1:aaa

## AND/OR commands

Though not really related to piping, it is nice to know that several commands can be executed on a single
line, with conditional execution using "&&" (AND), "||" (OR) .

    # use touch on file1 AND file2, touch file2 only if touch on file1 succeeds
    $ touch file1 && touch file2

    # use touch on file1, if failed echo an error
    $ touch file4 || echo "Ooopsss!"
