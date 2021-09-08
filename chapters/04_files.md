# Files and directories

Behind the scene, everything in Linux is a file (file, directory, port, etc.)

Files *usually* have extensions, but this is not mandatory.

you can get information on *file* type with the **file** commmand

    $ file file1
    file1: ASCII text, with CRLF line terminators
    $ file /home/user1
    .: directory

Linux files are case sensitive, and *should* not contain spaces in name

    $ ls File1
    will create an error

If name contains white spaces, name should be enclosed between single quotes

    $ touch 'my file with spaces'
    $ ls 'myfile with spaces'

Backspace can also be used to escape whitespace

    $ ls myfile\ with\ spaces

## Hidden files/directories

By default **ls** does not show hidden file.
Hidden files start with a dot (.config for example).

A *ls* in your home directory usually contains several hidden files (and more after some different installations...)

You can list hidden files with a *ls -a*

    $ ls
    file1 file2 subdir1
    $ ls -a
    file1 file2 subdir1 .bashrc  ...
    # or combined with long description option
    $ ls -la
    ...


## Find a file

The **find** command search through a directory and its subdirectories for a file name and/or type


    $ ls
    file1 file2 subdir1
    $ ls subdir1
    file1
    $ find . -type f   # search all files in current directory and subdirectories
    file1
    file2
    subdir1/file1
    $ find . -type f -name file1  # here we add condition on file name
    ./file1
    ./subdir1/file1