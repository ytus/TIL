# Linux

## Warning _The volume boot has only 0 bytes disk space remaining_

You have too many kernels installed. To remove the *old* ones:

> Get the current kernel version, the one you want to keep:

    `$ uname -r`

> Get the list of all kernels installed:

    `$ dpkg -l | grep linux-image-`

> Run apt-get remove on the kernels you want to remove. Not on the latest one! For example:

    `$sudo apt-get remove linux-image-2.6.32-22-generic`

(~ https://askubuntu.com/a/592135 )
