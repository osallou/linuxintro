# Processes

## What is Currently Running?

Linux, like most modern OS's is a multitasking operating system.
This means that many processes can be running at the same time.
As well as the processes we are running, there may be other users
on the system also running stuff and the OS itself will usually also
be running various processes which it
uses to manage everything in general.

If we would like to get a snapshot of what is currently happening on the system we may
use a program called **top**.

    $ top
    Tâches:   4 total,   1 en cours,   3 en veille,   0 arrêté,   0 zombie
    %Cpu(s):  6,2 ut,  3,3 sy,  0,0 ni, 90,4 id,  0,0 wa,  0,1 hi,  0,0 si,  0,0 st
    KiB Mem:   8347960 total,  5595908 used,  2752052 free,    34032 buffers
    KiB Swap: 25165824 total,   241200 used, 24924624 free.   188576 cached Mem

    PID UTIL.     PR  NI    VIRT    RES    SHR S  %CPU %MEM    TEMPS+ COM.
      1 root      20   0    9368    744    280 S   0,0  0,0   0:00.20 init
      8 root      20   0    8940    232    184 S   0,0  0,0   0:00.00 init
      9 user1   20   0   16524   3960   3856 S   0,0  0,0   0:00.82 bash
    152 user1   20   0   14636   1660   1144 R   0,0  0,0   0:00.01 top

You can leave with a Ctr+C

It shows useful information of top processes running, with cpu and memory information.

Top will give you a realtime view of the system and only show the number of processes which will fit on the screen.

Another program to look at processes is called ps which stands for processes.
In it's normal usage it will show you just the processes running in your current terminal (which is usually not very much).

If we add the argument *aux* then it will show a complete system view
which is a bit more helpful. *-ef* argument shows different information

    $ ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.0  0.0   9368   744 ?        Ssl  14:47   0:00 /init
    root         8  0.0  0.0   8940   232 tty1     Ss   14:47   0:00 /init
    user1      9  0.0  0.0  16524  3960 tty1     S    14:47   0:00 -bash
    user1    153  0.0  0.0  14312  1508 tty1     R    18:15   0:00 ps aux
    $ ps -ef
    UID        PID  PPID  C STIME TTY          TIME CMD
    root         1     0  0 14:47 ?        00:00:00 /init
    root         8     1  0 14:47 tty1     00:00:00 /init
    user1        9     8  0 14:47 tty1     00:00:00 -bash
    user1      155     9  0 18:17 tty1     00:00:00 ps -ef

The PID column is important as it is a way to refer to your running process

## Killing a Crashed Process

It doesn't happen often, but when a program crashes, it can be quite annoying, or program is too long (unexpected) and you wish to stop it.

Let's say we've got our browser running and all of a sudden it locks up.
You try and close the window but nothing happens, it has become
completely unresponsive.

No worries, we can easily kill Firefox and then reopen it.

To start off we need to identify the process id.

    $ ps aux | grep 'firefox'
    user1 6978 8.8 23.5 2344096 945452 ? Sl 08:03 49:53 /usr/lib64/firefox/firefox

It is the number next to the owner of the process that is the PID (Process ID).

We will use this to identify which process to kill.

To do so we use a program which is appropriately called kill.

    kill [signal] <PID>

    kill 6978

Sometimes you are lucky and just running kill normally will get the process
to stop and exit.

When you do this kill sends the default signal ( 1 ) to the process which
effectively asks the process nicely to quit.

We always try this option first as a clean quit is the best option.
Sometimes this does not work however.

No worries, we can run kill again but this time supply a signal of 9 which
effectively means, go in with a sledge hammer and make sure the process is
well and truly gone.

    kill -9 6978

## Process exit code

When a process ends, it exits with an exit code.
0 is successful, others usually mean an error
(some codes are standardized and have a meaning).

You can get the exit code of the program you launched with $?

    $ echo "hello"
    $ echo $?
    0

# Foreground and Background Jobs

You probably won't need to do too much with foreground and background jobs
but it's worth knowing about them just for those rare occassions.

When we run a program normally (like we have been doing so far) they are run in the foreground.

Most of them run to completion in a fraction of a second as well.

Maybe we wish to start a process that will take a bit of time and will
happily do it's thing without intervention from us
(processing a very large text file or compiling a program for instance).

What we can do is run the program in the background and then we can continue
working.

We'll demonstrate this with a program called **sleep**.
All sleep does is waiting for a given number of seconds and then quit.

We can also use a program called **jobs** which lists currently running
background jobs for us.

    $ sleep 5

If you run the above example yourself, you will notice that the terminal
waits 5 seconds before presenting you with a prompt again.

Now if we run the same command but instead put an ampersand ( & ) at the end
of the command then we are telling the terminal to run this process in the
background.

    $ sleep 5 &
    [1] 21634
    [1]+ Done sleep 5

This time you will notice that it assigns the process a job number (PID),
and tells us what that number is, and gives us the prompt back straight away.

We can continue working while the process runs in the background.

If you wait 5 seconds or so and then hit ENTER you will see a message come up
telling you the job has completed.

We can move jobs between the foreground and background as well.

If you press CTRL + z then the currently running foreground process will be
paused and moved into the background.

We can then use a program called **fg** which stands for foreground to bring
background processes into the foreground.

    $ fg <job number>

    $ sleep 15 &
    [1] 21637
    $ sleep 10
    (you press CTRL + z, notice the prompt comes back.)
    $ jobs
    [1]- Running sleep 15 &
    [2]+ Stopped sleep 10
    $ fg 2
    [1] Done sleep 15
