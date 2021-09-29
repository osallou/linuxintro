# SSH

Ssh is used to connect to a remote ssh server.

Connection can be with user/password or with your user identifier and a ssh key.

Using ssh key is more secure.

## Create a ssh key

To create a new key:

    ssh-keygen -t rsa

You *should* specify a password for your key, and not forget it!!!

This will, by default, generate 2 files:

    ~/.ssh/id_rsa
    ~/.ssh/id_rsa.pub

id_rsa file is your private key and should be accessible only by you!!!
id_rsa.pub is the public key, and can be shared with other users/servers.

To connect to a server with your key, the content of your public key should
be added to the remote server ~/.ssh/authorized_keys file.
Public key should be copied with care to be on a single line

## Using the key

Most ssh command allows to specify the private key to use via command-line:

    # connect to myremoteserver using my id_rsa private key
    $ ssh -i ~/.ssh/id_rsa  myremoteserver

To avoid specifying the key each time (and entering password of the key),
it is possible to use an ssh-agent

    $ ssh-add ~/.ssh/id_rsa
    # then follow instructions displayed on the screen

## Copying files over ssh

**scp** program copies files from/to a remote ssh server

    # copy local file1 to remote server in /home/user1 directory
    $ scp file1 myremoteserver:/home/user1/
    # copy remote /home/user1/file1 locally
    $ scp myremoteserver:/home/user1/file1 ./

**scp** support wildcards, recursive copies etc.,
see manual page for more information.

If your user identifier is different on remote server, yuo can specify it:

    $ scp file1 myuserid@myremoteserver:/home/user1/

*myremoteserver* is a remote server name or an ip address. In any case,
it needs to be reachable from your network.

This means, usually, that you can use scp from your computer to an external server, but not the
contrary because your computer IP address will not be reachable from the server as your IP address
is not a public one (but depends...).

## Testing

Have no ssh server to connect to for testing?

you create create a free account on github and follow instructions
to test a connection with your ssh key
[https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)