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

    [1]+  Stopped                 vim

use tis command:

    fg

(~ http://superuser.com/questions/268230/how-can-i-resume-a-stopped-job-in-linux )

## Find and kill a process that uses some port (`error: bind: Address already in use`)

Find the PID	

    fuser 8080/tcp 

or

    sudo netstat -tulpn

and kill it

    fuser -k 8080/tcp 

or 

    sudo kill -9 1234

(~ https://stackoverflow.com/a/11596144 )

## Setting an environment variable

For example `MAVEN_OPTS`: 

    export MAVEN_OPTS="-noverify -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n -Xnoagent -ea -Xmx1024m"

In Windows:

    set MAVEN_OPTS=-noverify -Xdebug -Xrunjdwp:transport=dt_socket,address=8000,server=y,suspend=n -Xnoagent -ea -Xmx1024m

## JetBrains IDE installation

> The recommended install location according to the filesystem hierarchy standard (FHS) is /opt. To install WebStorm into this directory, type the following command:

    sudo tar xfz WebStorm-*.tar.gz -C /opt/

> Switch to the bin subdirectory:

    cd opt/WebStorm-*/bin

> Run webstorm.sh from the bin subdirectory.

(~ https://www.jetbrains.com/help/webstorm/install-and-set-up-product.html)

## Slow Linux in VirtualBox

On Windows? Disable Deffender for the folder with your virtual machine and processes `VirtualBox` and `VirtualBox.exe`.

and then `Tools -> Create Desktop Entry...` to update desktop shortcuts.
