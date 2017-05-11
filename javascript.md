## Error `/usr/bin/env: ‘node’: No such file or directory` in Webstorm

When running a node package as an _External Tool_ in Webstorm (for example prettier), you can get this error:

> /usr/bin/env: ‘node’: No such file or directory

It may be caused by the way `nvm` changes your `PATH`, see: https://intellij-support.jetbrains.com/hc/en-us/community/posts/205964744-npm-is-installed-using-nvm-but-IntelliJ-doesn-t-know-about-it

If that's the case, there is a solution. Simply copy the two lines, that set path to node using nvm from your `~/.bashrc` 

~~~ bash
export NVM_DIR="/home/_you_/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm
~~~

into `~/.profile`.



## flow: polymorphic types and the error: `This type is incompatible with ... some incompatible instantiation of`

Polymorphic types are quite strict: 

> [...] polymorphic types exist to reference the same exact value through a function or class. 
> Not the type of value but the value or a modified version of the value itself.

~ https://github.com/facebook/flow/issues/2194#issuecomment-237899795
