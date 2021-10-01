# Navigation

## setup for exercices

We suppose here you are user *user1* and your home directory is */home/user1*, so simply replace */home/user1* by your user home directory in the following exercices/examples

To know what is your home directory:

    $ cd
    $ pwd
    /home/user1  <== this is your home directory

And replace /home/user1 by your personal home directory

Execute the following (don't worry you will understand after)

    $ cd
    $ mkdir -p /home/user1/subdir1
    $ touch /home/user1/file1
    $ touch /home/user1/file2
    $ touch /home/user1/subdir1/file1
    $ touch /home/user1/subdir1/file2
    $ touch /home/user1/subdir1/file3

## File hierarchy

File system starts at directory "/", the *root* of the system.
All paths use the "/" separator.

This usually looks like:

```
/
| bin
| usr
     | bin
| home
     | user
...
```

The "/" directory will contain other directories and files, themselves,
containing other directories and files.

To access a resource (a file or a directory) you will to give its path to the command
you execute. More information in **Path** chapter below.

An invalid path will raise an exception (No such file or directory)

## Where are we?

First command to know is the *pwd* command which indicates where we are
located in the file hierarchy.

    $ pwd
    /home/user1

## What's inside a directory

**ls** command list the files and directories

    $ ls
    file1 file2 subdir1

**ls** has options: ls [options] [location]

For example, to get detailed information of current directory

    $ ls -l
    total 3
    rwxr-xr-x  2 user1 team1 4096 Mar 23 13:34 file1
    rwxr-xr-x 18 user1 team1 4096 Feb 17 09:12 file2
    drwxr-xr-x  2 user1 team1 4096 May 05 17:25 subdir1

Specifying location to look at:

    $ ls -l /home/user1
    total 3
    rwxr-xr-x  2 user1 team1 4096 Mar 23 13:34 file1
    rwxr-xr-x 18 user1 team1 4096 Feb 17 09:12 file2
    drwxr-xr-x  2 user1 team1 4096 May 05 17:25 subdir1

First character indicates whether it is a normal file ( - ) or
directory ( d )

Next 9 characters are permissions for the file or directory
(more about them in [permissions]09_permissions.md)).

The next field is the number of blocks (don't worry too much about this).

The next field is the owner of the file or directory (user1 in this case).

The next field is the group the file or directory belongs to (team1 in this case).

Following this is the file size.

Next up is the file modification time.

Finally we have the actual name of the file or directory.

## Path

A path defines where a file or directory is located on the system,
it can be relative or absolute.

Absolute paths specify a location (file or directory) in relation to the root directory. You can identify them easily as they always begin with a forward slash ( / )

Relative paths specify a location (file or directory) in relation to where we currently are in the system. They will not begin with a slash.

Example:

    $ pwd
    /home/user1
    # show relative path content of subdir1
    $ ls subdir1
    file1.txt file2.txt file3.txt

    # show content of specified path
    $ ls /home/user1/subdir1
    file1.txt file2.txt file3.txt

Using absolute or relative path is "up to you"....
Sometimes it is shorter to use relative path rather than writing the full path,
but it can also be less readable or you may be unsure of final location.

Extra ways exist to navigate in relative path:

* ~ (tilde) - This is a shortcut for your home directory. eg, if your home directory is /home/user1 then you could refer to the directory Documents with the path */home/user1/Documents* or *~/Documents*
* . (dot) - This is a reference to your current directory. eg in the example above we referred to subdir1 with a relative path. It could also be written as ./subdir1 (Normally this extra bit is not required but in later sections we will see where it comes in handy).
* .. (dotdot)- This is a reference to the parent directory. You can use this several times in a path to keep going up the hierarchy. eg if you were in the path /home/user1 you could run the command ls ../../ and this would do a listing of the root directory.

    # go to home directory with *cd*, see following chapter
    $ cd
    $ ls /home/user1/subdir1
    file1.txt file2.txt file3.txt
    $ ls ../../  (show 2 levels up in the directory hierarchy)
    bin boot dev etc home lib var
    $ ls /  (show root directory content)
    bin boot dev etc home lib var

## moving between directories

The **cd** command moves to the specified directory location:  cd [location]

    $ cd /
    $ pwd
    /
    $ ls
    bin boot dev etc home lib var
    cd ~/subdir1
    $ pwd
    /home/user1/subdir1
    $ cd ../../
    $ pwd
    /home
    $ cd
    $ pwd
    $ /home/user1

## disk usage

*df* command shows the different disks usage (physical or virtuals/remote)

Option -h will show usage in human readable values (megabytes, giga, ..)
instead of number of blocks

    $ df -h
    Filesystem                   Size  Used Avail Use% Mounted on
    devtmpfs                      16G     0   16G   0% /dev
    tmpfs                         16G  445M   16G   3% /dev/shm
    tmpfs                        6.3G  2.4M  6.3G   1% /run
    /dev/nvme0n1p2                96G   72G   20G  79% /
    tmpfs                         16G   13M   16G   1% /tmp
    /dev/nvme0n1p1               200M   36M  165M  18% /boot/efi
    /dev/dm-0                    357G  213G  127G  63%
    //some-remote/user1   12G  208M   12G   2% /mnt/user1   <== a remote volume

*du* will calculate the disk usage in a directory and its subdirectories.
This command will parse all dir/sub dirs so can be quite long to execute
depending on number fo files/dirs.

Example:

    $ du -h .
    104K    ./chapters <= size of sub directory chapters
    64K	./.git/hooks
    8.0K	./.git/info
    8.0K	./.git/objects/b6
    ...
    648K	.  <= total of current and sub directories content

It is possible to limit the display output to a number of directory depth with *--max-depth* option

        # Show only total
        $ du -h --max-depth 0 .
        648K	.
        # show only current dir and direct subdirs totals
        104K	./chapters
        528K	./.git
        648K	.

## tips

The *tab* key helps for autocompletion.

you can try

    cd /home/us<TAB>

which should complete command to /home/user1.
