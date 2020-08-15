---
layout: default
title: Build Small Telegram xkcd Bot in Clojure
---
# Bacgkround
Clojure is one of language i learnt last year. After learning through Clojure for the Brave and True ebook, i didn't able to use it properly.
My first project to build online shop website stop only in 3 weeks. I found my skill not adequate to just create website CRUD. After that, I didn't touch clojure until May 2020.
Avoiding my fall in in first project, i plan build much simpler that i can do in my spare time, around 5 hours a week. Others requirement:
- no time limit, but feature scoped to minimum.
- can make simple outgoing request
- respond limited incoming request with response
- serve one small functionality
As I browsing net, I remember my interest in learning Telegram's bot. I decide building small comic bot to get latest comic fulfill my requirements. A

# Looking API
Thanks to [list of public apis](https://github.com/public-apis/public-apis), I easily find xkcd has free API. And, I like reading xkcd too.

# Setup Project
Clojure has several tools that can be used as starting point: Leinengen, Boot, and Deps. Those three are not same things but fulfill my needs to download dependency, build, run, and deploy later. As I am newbie, I decide to use Deps as I find it very minimum. Leinengen and Boot has wide features which I don't need it right now.
1. create project directory
1. create deps file
1. dependency can be added under aliase :deps map. I put popular (clj-http)[https://github.com/dakrone/clj-http] as first dependency.

# REPL for interactive test
REPL create smooth experience while explore api request and response. It is easy to boot clojure repl with deps by invoke `clj` in root project.

# Setup Test Runner
Since introduced with TDD in my workplace in 2015, I find practicing TDD is very helpful in development and after. It gives set of thinking model to verify anything. And becomes safety net later when doing any changes. You get free sort of documentation. Of course, it doesn't mean it always result good things. Tools are as good as the wielder.
Because of that, first thing I look is how setup testing. In Android, I use jUnit4 runner. Here we can use clojure.test. But I use [kaocha](https://github.com/lambdaisland/kaocha) which the first runner I successfully setup.
