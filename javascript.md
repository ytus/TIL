## Error `/usr/bin/env: ‘node’: No such file or directory` in Webstorm

When running a node package as an _External Tool_ in Webstorm, you can get this error:

> /usr/bin/env: ‘node’: No such file or directory

To workaround it, launch Webstorm from terminal, for example:

> $  /home/<you>/Downloads/WebStorm-163.7743.51/bin/webstorm.sh

(That path is in `~/.local/share/applications/jetbrains-webstorm.desktop`.)

## flow: polymorphic types and the error: `This type is incompatible with ... some incompatible instantiation of`

Polymorphic types are quite strict: 

> [...] polymorphic types exist to reference the same exact value through a function or class. 
> Not the type of value but the value or a modified version of the value itself.

~ https://github.com/facebook/flow/issues/2194#issuecomment-237899795
