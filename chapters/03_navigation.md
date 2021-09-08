# Navigation

## setup for exercices

We suppose here you are user *user1*, simply replace user1 by your user id in the exercices/examples

Execute the following (don't worry you will understand after)


    $ cd
    $ mkdir -p /home/user1/subdir1
    $ touch /home/user1/file1
    $ touch /home/user1/file2
    $ touch /home/user1/subdir1/file1
    $ touch /home/user1/subdir1/file2
    $ touch /home/user1/subdir1/file3



## File hierarchy

File system starts at "/", the *root* of the system.
All paths use the "/" separator.

```
/
| bin
| usr
     | bin
| home
     | user
...
```

## Where are we?

First command to know is the *pwd* command which indicates where we are
located in the file hierarchy.

   $ pwd
   /home/user1

## What's inside directory

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

First character indicates whether it is a normal file ( - ) or directory ( d )

Next 9 characters are permissions for the file or directory (we'll learn more about them in [permissions]09_permissions.md)).

The next field is the number of blocks (don't worry too much about this).

The next field is the owner of the file or directory (user1 in this case).

The next field is the group the file or directory belongs to (team1 in this case).

Following this is the file size.

Next up is the file modification time.

Finally we have the actual name of the file or directory.

## path

 A path is a mean to get to a particular file or directory on the system, it can be relative
 or absolute

Absolute paths specify a location (file or directory) in relation to the root directory. You can identify them easily as they always begin with a forward slash ( / )

Relative paths specify a location (file or directory) in relation to where we currently are in the system. They will not begin with a slash.

Here's an example to illustrate:

    $ pwd
    /home/user1
    # show relative path content
    $ ls subdir1
    file1.txt file2.txt file3.txt

    # show content of specified path
    $ ls /home/user1/subdir1
    file1.txt file2.txt file3.txt

Extra ways exist to navigate in relative path:

* ~ (tilde) - This is a shortcut for your home directory. eg, if your home directory is /home/user1 then you could refer to the directory Documents with the path /home/user1/Documents or ~/Documents
* . (dot) - This is a reference to your current directory. eg in the example above we referred to subdir1 with a relative path. It could also be written as ./subdir1 (Normally this extra bit is not required but in later sections we will see where it comes in handy).
* .. (dotdot)- This is a reference to the parent directory. You can use this several times in a path to keep going up the hierarchy. eg if you were in the path /home/user1 you could run the command ls ../../ and this would do a listing of the root directory.


    $ cd  (go to home directory, see after)
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

## tips

The *tab* key helps for autocompletion.

you can try

    cd /home/us<TAB>

which should complete command to /home/user1