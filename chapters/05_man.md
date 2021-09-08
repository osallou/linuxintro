# Man

The *man* command is useful to get manual page of a software.
Be aware though that not all softwares provide a man page.

Man pages are formatted files installed on the system with the description and options of the software, usually named mysoftware.1, mylib.3

    $ man ls
    Name
        ls - list directory contents
    
    Synopsis
        ls [option] ... [file] ...
    
    Description
        List information about the FILEs (the current directory by default). Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.
    
        Mandatory arguments to long options are mandatory for short options too.
    
        -a, --all
            do not ignore entries starting with .
    
        -A, --almost-all
            do not list implied . and ..
