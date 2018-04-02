---
layout: default
title: (Not) Naive MD5
---
What is MD5
===========
It is one of hashing techniques

Naive implementation
--------------------
based on RFC 1321, peek and copy from [Github](https://github.com/CastixGitHub/racket-md5), and pseudocode at [Wikipedia](https://en.wikipedia.org/wiki/MD5).
Code in Racket could be found [here](https://github.com/binilinlquad/md5/tree/v0.1).
This implementation cannot processing message bigger than provided memory because it is trying to put whole message into memory.

Better implementation with Port
-------------------------------
The algorithm only need processing 64 bytes block each time, then we doesn't need all data in memory.
We only need to customise input port to include extra padding and message length.
[Source Code](https://github.com/binilinlquad/md5/tree/v0.2)

Expose Digest Functions to User
-------------------------------
Provides functions `digest-bytes`, `digest-string`, and `digest-file` for user. To use it, just `(require "./md5.rkt")` if the file is in same directory.
[Source Code](https://github.com/binilinlquad/md5/tree/v0.3)
