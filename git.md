## Undo `git add some/file.txt`

>     $ git reset HEAD some/file.txt

(~ https://stackoverflow.com/a/348303 )

## Extract a single file from stash

>     $ git checkout stash@{0} -- <filename>

(~ https://stackoverflow.com/a/1105666 )

## How to find when was a file deleted

> git log -- */fileName.xyz

or, if it shows nothing: 

> git log --full-history */fileName.xyz

Thanks to `*/` you don't have to write the full path to the file and `--full-history` will force git to skip "history simplification", see: http://stackoverflow.com/a/34755406 .

## bisect (binary search)

Tell git which commit is certainly `good` and which is certainly `bad`, then chceck, whether offered commits are `good` or `bad` (and tell this to `git`). To stop use `reset`.

To see (or check or test...) a specific commit use `$ git checkout ABCDEF`.

~~~ bash
$ git bisect start
$ git bisect good fd0a623
$ git bisect bad 256d850
(...)
$ git bisect good/bad
(...)
$ ABCDEF is the first bad commit
$ git bisect reset
~~~

# shorter way to push new branch `git push --set-upstream origin some-branch`

Instead of this:

> git push 
> fatal: The current branch fa-319-schema-instead-of-code has no upstream branch.
> To push the current branch and set the remote as upstream, use
>   git push --set-upstream origin fa-319-schema-instead-of-code
    
Use this:    

> git push -u origin HEAD    
