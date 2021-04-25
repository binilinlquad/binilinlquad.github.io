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

*Spawn nRepl*
Put nrepl setting inside `:nrepl` inside your lein `project.clj`, so it looks like this:
```
(defproject project-name "0.1.0-SNAPSHOT"
  :dependencies [[org.clojure/clojure "1.10.0"]
                 [ring/ring-core "1.7.1"]]
  :plugins [[lein-ring "0.12.5"]]
  :ring {:handler your-ring-handle-function
         :nrepl {:start? true
                 :port 9000}})
```
Sample above will start nRepl in `localhost` with port 9000. Connect with to nRepl with your favorite tool. If you use Cider like me, connect using `cider-connect-nrepl`.

*Request*
Ring's http request (request)[https://github.com/ring-clojure/ring/wiki/Concepts#requests] is clojure map and it is same for (response)[https://github.com/ring-clojure/ring/wiki/Concepts#responses].
