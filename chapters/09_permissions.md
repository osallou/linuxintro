# Permissions

Linux permissions dictate 3 things you may do with a file,
read, write and execute.
They are referred to in Linux by a single letter each.

* r read - you may view the contents of the file.
* w write - you may change the contents of the file.
* x execute - you may execute or run the file if it is a program or script.

For every file we define 3 sets of people for whom we may specify permissions.

* owner - a single person who owns the file. (typically the person who created the file but ownership may be granted to some one else by certain users)
* group - every file belongs to a single group.
* others - everyone else who is not in the group or the owner.

Three persmissions and three groups of people.
That's about all there is to permissions really. 
Now let's see how we can view and change them.

## View permissions

    $ ls -l
    total 3
    rwxr-xr-x  2 user1 team1 0 Mar 23 13:34 file1
    rwxr-xr-x 18 user1 team1 0 Feb 17 09:12 file2
    drwxr-xr-x  2 user1 team1 4096 May 05 17:25 subdir1

The first character identifies the file type.
If it is a dash ( - ) then it is a normal file.
If it is a d then it is a directory.

The following 3 characters represent the permissions for the owner.
A letter represents the presence of a permission and a dash ( - ) represents the absence of a permission.

In this example the owner has all permissions (read, write and execute).

The following 3 characters represent the permissions for the group.
In this example the group has the ability to read but not write or execute.

Note that the order of permissions is always read, then write then execute.

Finally the last 3 characters represent the permissions for others (or everyone else).
In this example they have the execute permission and nothing else.

For a directory, a *x* permission means the permission to enter the directory.

## Change permissions

To change permissions on a file or directory we use a command called chmod.

    chmod [permissions] [path]

chmod has permission arguments that are made up of 3 components

Who are we changing the permission for? [ugoa] - user (or owner), group, others, all

Are we granting or revoking the permission - indicated with either a plus ( + ) or minus ( - )

Which permission are we setting? - read ( r ), write ( w ) or execute ( x )

The following examples will make their usage clearer.

Grant the write permission to the group. Then remove the write permission for the owner.

    $ ls -l file1
    rwxr-xr-x  2 user1 team1 4096 Mar 23 13:34 file1
    $ chmod g+w file1
    $ ls -l file1
    rwxrwxr-x  2 user1 team1 4096 Mar 23 13:34 file1
    $ chmod u-w file1
    $ ls -l file1
    r-xrwxr-x  2 user1 team1 4096 Mar 23 13:34 file1

*tip* one can use octal syntax to set permissions (won't detail here).
For example *chmod 755 filename* will set rwx r-x r-x acls.