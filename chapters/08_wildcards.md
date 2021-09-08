# Wildcards and globbing

Wildcards are a set of building blocks that allow you to create a pattern
defining a set of files or directories. As you would remember, whenever we
refer to a file or directory on the command line we are actually referring
to a path. Whenever we refer to a path we may also use wildcards in that
path to turn it into a set of files or directories.

Here is the basic set of wildcards:

* \* - represents zero or more characters
* ? - represents a single character
* [] - represents a range of characters


    $ ls
    file1 file2 dir1
    ls f*
    file1 file2

Wildcard is interpreted meaning that command is transformed
before being passed to the program. This means that "ls f*" will make system look for "f*" matches and run "ls file1 file2". If command does not support multiple arguments this will fail.

Example:

    # I have a program named myprogram which expects a single argument
    $ myprogram f*
    # you will get an error because what is executed is myprogram file1 file2


In this example we have used an absolute path.
Wildcards work just the same if the path is absolute or
relative.

    $ cd
    $ touch file1.txt
    $ touch file2.txt
    $ touch other1.txt
    $ touch other.mpeg
    $ ls /home/user1/*.txt
    /home/user1/file1.txt /home/user1/file2.txt  /home/user1/other1.txt


Now let's introduce the ? operator.
In this example we are looking for each file whose second letter is i
 As you can see, the pattern can be built up using several wildcards.

    $ ls ?i*
    file1.txt file2.txt


Or how about every file with a three letter extension. Note that other.mpeg is not matched as the path name must match the given pattern exactly.

    $ ls *.???
    file1.txt file2.txt other1.txt


And finally the range operator ( [ ] ).
Unlike the previous 2 wildcards which specified any character, the range operator allows you to limit to a subset of characters.

In this example we are looking for every file whose name either begins with a f or o.

    $ ls [fo]*
    file1.txt file2.txt other1.txt

With ranges we may also include a set by using a hyphen. So for example if we wanted to find every file whose name includes a digit in it we could do the following:

    $ ls *[0-9]*
    file1.txt file2.txt other1.txt

We may also reverse a range using the caret ( ^ ) which means look for any character which is not one of the following.

    $ ls [^a-k]*
    other1.txt other.mpeg
