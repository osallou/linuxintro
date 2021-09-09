# File manipulations

## Create a directory

Command **mkdir** creates directories

    $ mkdir nameofdir
    $ mkdir nameofdir/nameofsubdir

To create a directory, sub directories must already exist.

To force create a full directory path, creating sub directories if they do not exists

    $ mkdir -p dir1/dir2/dir3

## Remove a directory

**rmdir** deletes a directory if directory is empty.

    $ rmdir dir1/dir2/dir3
    $ rmdir dir1/dir2
    $ rmdir dir1

## Create an empty file

**touch** creates a file with empty content or,
if it exists, updates its last modification time.

    $ touch file4

## Copy files

**copy** copy one or more files to a destination directory: cp [options] source destination

    # copy file1 to a new file file2 (replace if exists)
    $ cp file1 file2
    $ mkdir dir1
    # copy file1 with the same name in directory dir1
    $ cp file1 dir1/

When we use cp the destination can be a path to either a file or directory.
If it is to a file then it will create a copy of the source but name the copy
 the filename specified in destination.
If we provide a directory as the destination then it will copy the file into that directory and the copy will have the same name as the source.

In it's default behaviour cp will only copy a file (there is a way to copy several files in one go but we'll get to that in chapter [Wildcards](08_wildcards.md)).

Using the -r option, which stands for recursive, we may copy directories.

Recursive means that we want to look at a directory and all files and
directories within it, and for subdirectories, go into them and do the same
thing and keep doing this.

    $ ls
    file1 dir1
    $ mkdir dir1/subdir1
    $ touch dir1/file1
    $ touch dir1/file2
    $ touch dir1/subdir1/subfile1
    $ mkdir dir2
    # copy content of dir1 recursivly in dir1
    $ cp -r dir1 dir2
    $ ls dir2
    file1 file2 subdir1
    $ ls dir2/subdir1
    subfile1

## Moving files or directories

To move a file we use the command mv which is short for move.
It operates in a similar way to cp.
One slight advantage is that we can move directories without having to
provide the -r option.

   $ ls
   file1 dir1 dir2
   $ mv dir1 dir3
   $ ls
   file1 dir2 dir3

## Rename

Well... simply use **mv**!

  $ ls
  file1
  $ mv file1 newfile1
  $ ls
  $ newfile1

## Delete a file and non empty directories

**rm** command is the  key ;-)  rm [options] file

**warning** A rm is definitive, no way back with a trash where you cuold restore file!!!

    $ ls
    file1 file2
    $ rm file1
    $ ls
    file2

To delete a non empty directory, simply use the *-rf* option

    $ ls
    file1
    $ mkdir dir1
    $ ls
    file1 dir1
    $ touch dir1/file1
    $ rm -rf dir1
    $ ls
    $ file1

The -r is for recursive, and -f for force.

**rm** command accepts multiple file path for deletion, for example:  rm file1 file2 file3

**warning** the -r command is dangerous, mainly if you have root access as
you may delete important directories (operating system) with no way back

**warning** for a recursive deletion **always** check twice the path of the
directory in the command. A "*" or a whitespace badly placed could lead to
unwanted deletion....
