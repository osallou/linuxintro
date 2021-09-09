# Linux

## Good to know

In following examples, the terminal prompt will be "$" (first character of the line).
This means that you should not copy this "$" in your terminal to reproduce the examples.
Lines not starting with $ represent the output of the commands

For example:

    $ echo "hello"     <= You should only write  *echo "hello"* in your terminal
    hello              <= this is what appears in your terminal

## Kernel

The Linux kernel is the main component of a Linux operating system (OS) and is the core interface between a computer’s hardware and its processes. It communicates between the 2, managing resources as efficiently as possible.

The kernel is so named because—like a seed inside a hard shell—it exists within the OS and controls all the major functions of the hardware, whether it’s a phone, laptop, server, or any other kind of computer.

## What the kernel does

The kernel has 4 jobs:

* Memory management: Keep track of how much memory is used to store what, and where
* Process management: Determine which processes can use the central processing unit (CPU), when, and for how long
* Device drivers: Act as mediator/interpreter between the hardware and processes
* System calls and security: Receive requests for service from the processes

## Graphical interface and command-line

Linux OS provides desktop interface like Windows, but also a command-line with interpreters
(bash, zsh for a few) to navigate, execute processes and scripts.

Servers are usually command-line only, i.e. the system is installed without the desktop graphical
packages, and can be accessed remotly via **ssh**. Once connected via ssh, user is connected
to a command-line environement only.

Graphical interfaces are run by *X server* or *Wayland*.

## Users

Multiple users can use/connect to a linux system and operate in parallel.

Each user has a user id (*uid*) and a main group id (*gid*) with specific rights.
Ids are numeric values, but usually have string aliases displayed by the system to be
more human readable and usable (who remembers ids...?)

A default super user is created at installation, the **root** user with uid=0, gid=0.
This user is used by the operating system to boot and start most system processes.

**root* super user has all rights on the system. He can create/delete users, modify any user resource, kill any process etc.

A user can switch to a different one (if allowed), so user A can for example switch to root at
any time to execute priviledged commands then go back to its role. The *sudo* command can also
help to run a specific command as *root* (user need of course to have the right to execute sudo).

The *group* id is the main group of a user. Users in a same group can share some resources
(files or directories). By default, a new file/directory will be created with user id and gid.
More details in [files.md] chapter.

User can also have extra groups, also called secondary groups. Their use is the same as the main group.
User a can for example have main group *users* be in other secondary groups *team1*/*team2*.

    $ id   # show current user id/groups
    uid=1046(userA) gid=20857(users) groups=20857(team1),989(docker),40687(admins)

As user can switch between different user id/roles, might be interesting to know which user you are ;-)

    $ whoami
    userA

Each user has a *home* directory, usually (but not necessarly) in /home. This *home* is owned
by the user and is writable by the user.

Other system directories will *mostly* accessible by root user only (but directory /tmp)

## Operating system

As explained above, linux is the kernel, and the distribution had everyting what is needed behind
to make it *useful* as a user/developper/adminstrator (a shell, a deskop, editors, ...).

At boot, the kernel starts and launch an init system. Most of distributions, today, use **systemd**.
In a (very) short, systemd read a list of service definition. Some definitions request to be started
at boot. Other services may be started on-demand or time based.
Systemd will also check services are in expected state and *try* to reconcile if possible.

Some services are set with the distribution, but with root privileges, it is also possible to add
your own definitions to add a new service to be started at boot for example.

Available with a number of packages/softwares, *root* user can install extra softwares via a
package manager (depends on distribution, apt for debian based, dnf for fedora/centos)

For example to install the vim editor

    # debian
    # refresh list of remote package repositories
    # apt-get update
    # apt-get install vim

    # fedora
    # dnf install vim

A user with no priviledges won't be able to install extra softwares with the package manager.

It is however possible to download the source of the software, compile it (if you have a compiler
installed) and run it in a user directory.

Package managers connect by default to remote repositories, but may not contain the software you
expect. Additional repositories can be added to expend the list of available software and
automate their update.

Depending on distribution, releases are frequent or not, and will impact the version of available
software as well as global system stability. The more *stable* system, the less recent software
versions....

## Disks

Unlike Windows, there is no *drive* in linux.
There are partitions (different filesystems can be used). Each partition will contain file/directories
and be size limited (but independently). A partition can be linked to a *physical disk* or be *logical*.

Navigating among the different disks (physical, logical, remote) will simply be like if you had
a single drive, it is only of matter of directories.

A full partition (no more space available) will not impact other partitions.

However, in most cases, the "/" partition contains the system libraries, cache etc., and if full
the whole system will be unusable.

If the user home directories are located in the same partition than the base partition, filling your
home may lead to a *broken* system, this is why home directories are usually set in a different partition.

Linux can also *mount* network disks (student home in a university for example is shared via the network
to access it from different computes, shared data directory in a company).
Network disk are mounted as a directory, but will be visible as a different partition

Example:

    $ df -h
    Filesystem                   Size  Used Avail Use% Mounted on
    devtmpfs                     3.8G     0  3.8G   0% /dev
    tmpfs                        3.8G     0  3.8G   0% /dev/shm
    tmpfs                        3.8G  410M  3.4G  11% /run
    tmpfs                        3.8G     0  3.8G   0% /sys/fs/cgroup
    # The main partition with all system config, libraries, etc.
    /dev/mapper/cl_userA-root    50G   37G   14G  74% /
    /dev/vda1                    976M  243M  667M  27% /boot
    # location of all users home on a remote server, mounted on local directory /home
    networkshares:/home          80T   13T   68T  16% /home
    # some shared data on a remote server, mounted on local directory /mnt/data
    networkshares:/shareddata    650T  531T  120T  82% /mnt/data

## Logs

Systemd and most of services generate logs. When something is wrong, a good place to look at is
/var/log.

This directory will have many log files, possibly with rotation (date or size constrained), with
system related information in /var/log/messages or /var/log/syslog.

## Good to know

As a developper, you will need to connect to remote servers. Though remote connections can be
done via basic user/password authentication, most systems require *ssh* access with [*ssh keys*](ssh.md).
This make use of cryptographic solutions more secure than password usage.
This is also true for VCS (git, etc.) that makes use of behind-the-scene ssh use.

So you will need to create and know how to use ssh keys in your daily "work".

Signing stuff is also interesting (mandatory sometimes) and you may be interested by [GPG](https://gnupg.org/). GPG is a bit complex but worth a try or a look.

To install software, when you have no root priviledge, there are different tools that helps to
install stuff in your home and update the known *PATH* to find it.
[Conda](https://docs.conda.io/en/latest/) is a good example but not the only one.
