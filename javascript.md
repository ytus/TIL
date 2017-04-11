## Error `/usr/bin/env: ‘node’: No such file or directory` in Webstorm

When running a node package as an _External Tool_ in Webstorm, you can get this error:

> /usr/bin/env: ‘node’: No such file or directory

To workaround it, launch Webstorm from terminal, for example:

>  /home/<you>/Downloads/WebStorm-163.7743.51/bin/webstorm.sh

(That path is in `~/.local/share/applications/jetbrains-webstorm.desktop`.)

