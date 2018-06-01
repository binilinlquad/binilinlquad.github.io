---
layout: default
title: Learning Clojure Ring
---
*Background*
I've created simple inventory website for personal use in Python and Django. I've able to setup in short time. Because of not spending time for learning Python or Django properly, i find myself hardly able to implement new feature.
To not repeat same mistake, i choose to reimplement using JVM-based language which i have basic knowledge. I tried to build it using libraries not framework to understand how it works actually.

Notes:
This post purpose is to documented my journey in creating simple website with CRUD.

*Setup*
Ingredients:
1. Emacs and (Cider)[https://github.com/clojure-emacs/cider]
1. [Ring](https://github.com/ring-clojure/ring) which people saying default choice for web development.
1. [Leiningen](https://github.com/technomancy/leiningen) is for automating Clojure projects without setting your hair on fire (Quoted from the same website).
1. [lein-ring](https://github.com/weavejester/lein-ring/) for auto-reload and it provides nrepl too. I can connect with [Cider](https://github.com/clojure-emacs/cider)

*Steps*
1. Learning (Clojure for the Brave and True)[https://www.braveclojure.com/]
1. Create Ring project with Leinengen. It is in Ring Wiki.
1. Install lein-ring plugin. See Readme in lein-ring
1. Startup by `lein ring server`
1. Ask lein-ring to run nRepl. See Readme again.
1. Connect cider to running nRepl by `cider-connect-nrepl`
1. Run all test from cider by evaluate and run `(run-tests)` or `lein tests`
1. Implement, test, implement

*Request*
Ring's http request (request)[https://github.com/ring-clojure/ring/wiki/Concepts#requests] is clojure map and it is same for (response)[https://github.com/ring-clojure/ring/wiki/Concepts#responses].
