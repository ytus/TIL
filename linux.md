# Linux

## Warning _The volume boot has only 0 bytes disk space remaining_

You have too many kernels installed. To remove the *old* ones:

> Get the current kernel version, the one you want to keep:

    $ uname -r

> Get the list of all kernels installed:

    $ dpkg -l | grep linux-image-

> Run apt-get remove on the kernels you want to remove. Not on the latest one! For example:

    $sudo apt-get remove linux-image-2.6.32-22-generic

(~ https://askubuntu.com/a/592135 )


## Ctrl-S in a terminal

> How to unfreeze after accidentally pressing Ctrl-S in a terminal?

> Ctrl-Q is indeed the answer.

(~ http://unix.stackexchange.com/a/12146 )

## Ctrl-Z in a terminal

To resume a stopped process in Linux (when you press `Ctrl+Z`), for example:

> [1]+  Stopped                 vim

use tis command:

> fg

(~ http://superuser.com/questions/268230/how-can-i-resume-a-stopped-job-in-linux )

## Find and kill a process that uses some port

Find the PID	

> fuser 8080/tcp 

and kill it

> fuser -k 8080/tcp 

(~ https://stackoverflow.com/a/11596144 )
