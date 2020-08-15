---
layout: default
title: (TIL) Troubleshoot ktlint cannot Find java
---
Having consistent code style in team will make review others code easier. With that in mind, team decide to use [ktlint](https://github.com/pinterest/ktlint). [Installation steps](https://github.com/pinterest/ktlint#installation) helps setup instantly.

Because we are lazy to run it manually, we install git pre-commit hook as explained in [usages section](https://github.com/pinterest/ktlint#usage)
```
$ ktlint installGitPreCommitHook
``` 

It works flawlessly in terminal. Then I enable it in Android Studio by enable `Run Git hooks` in [Commit Dialog](https://i.stack.imgur.com/YPyPv.png). I am suprised when commit failed with messages telling that `ktlint` cannot find `java`. 
It is baffled me as I have setup java enviroment and add it to `PATH` in bashrc file. As Android Developer, it is first thing to do. I lookt at ktlint issues and internet, but cannot find people experiencing the same issue. 

Without any clue except Android Studio cannot find `java` then I try to look what is git pre-commit hook content. 
```
#!/bin/sh

# https://github.com/shyiko/ktlint pre-commit hook
git diff --name-only --cached --relative | grep '\.kt[s"]\?$' | xargs ktlint --relative .
if [ $? -ne 0 ]; then exit 1; fi
```

It clearly shows Android Studio can find `ktlint` which reside inside `/usr/local/bin`. I suspect Android Studio doesn't aware set `PATH` inside bashrc file but aware anything inside `/usr/local/bin`. I reluctant to move `java` to `/usr/local/bin`. Then I remember that we can make soft link  by running:
```
ln -s `which java` /usr/local/bin/java
```

After make sure soft link is working, I try commit with `Run Git Hooks` enabled in Android Studio again and now ktlint can find `java`  and works normally.

*My Environment*
1. Ubuntu 20.04 LTS
1. Android Studio 4.0
1. Bash with set `JAVA_HOME` and add `java` to `PATH`

*Thanks*
1. I got screenshot of `Run Git hooks` from [StackOverflow question](https://stackoverflow.com/questions/53607355/intellij-before-commit-run-git-hooks).  
2. ktlint for easy to setup and use. 
 
