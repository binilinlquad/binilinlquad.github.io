---
layout: post
title: Build Small Telegram xkcd Bot in Clojure
---
# Background
Clojure is one of languages I am learning since 2 years ago irregularly. Now is time to practice it through toy project. The project has these requirements:
- can be done in my spare time 
- no time limit, but feature is scoped to minimum
- make simple outgoing request
- respond to limited incoming request 
- serve one small functionality

With these in my mind, I remember my interest in learning Telegram's bot. I decide building a bot to get latest comic.

# Preparations
## Looking Comic API
Thanks to [list of public apis](https://github.com/public-apis/public-apis), I like reading xkcd and find it provides [endpoint](https://xkcd.com/info.0.json) which will give latest comic strip's information in json document. Try click the endpoint to see the result.

## Learning Telegram API
Surely I neead to learn [Telegram API](https://core.telegram.org/) because it is Telegram's bot at end of day. Telegram provides two way to let bot get latest chat messages :
- [Webhook](https://core.telegram.org/bots/api#setwebhook)
- Polling using [GetUpdates](https://core.telegram.org/bots/api#getting-updates)

Webhook needs my bot to be reachable by Telegram. As I want to focus core features to deliver latest comic strip to reader, I decide to use polling. The bot will poll every 5 minutes to get latest Telegram chats and deliver strip to people asking it.

I won't dwell too much because you can read directly in link that I put above. Just make sure to register your own bot before trying any APIs.

![Overview Diagram Flow for The Bot](/assets/overview-xkcd-bot-diagram-flow.png)

## Setup Build Tool
Clojure has several tools that can be used as starting point: Leinengen, Boot, and Deps. Those three are not exactly same things but fulfill my needs to :
1. download dependencies
2. build and create self contained jar
3. run application and run test

I decide to use [deps.edn](https://clojure.org/guides/deps_and_cli) as it is enough to fulfill my needs right now.

### Add Http Client
First I need http client to make HTTP request to xkcd. [clj-http](https://github.com/dakrone/clj-http) is popular choice by lot of people. To add dependency, add deps map of dependency in `deps.edn` file. The entry can be searched easily in [clojars](https://clojars.org/)
. The result will be like this
```clojure
{:deps 
 {clj-http/clj-http {:mvn/version "3.10.1"}}
}
```

### Setup Test Runner
Since introduced with TDD in workplace at 2015, I find practicing TDD is very helpful in development and after. It gives set of thinking way to verify anything. You get some sort of documentation if doing it rightly. Of course, it is only one of good practices.

Because of that, I look how setup test runner. I can use clojure.test here but, decide to use [kaocha](https://github.com/lambdaisland/kaocha) as I find kaocha's tutorial is very easy to follow.

Add test alias in deps.edn. I put my tests under `test` folder. 
```clojure
{:deps 
 {clj-http/clj-http {:mvn/version "3.10.1"}}

 :aliases
 {:test {:extra-paths ["test"]
         :extra-deps {lambdaisland/kaocha {:mvn/version "1.0.632"}}}}
}
```

Then create `bin/kaocha` under project folder as stated in [kaocha installing page](https://cljdoc.org/d/lambdaisland/kaocha/1.0.700/doc/2-installing) to make running test from command line easy. 

Try execute `bin/kaocha` to make all creted tests. If you want to run specific test, you will be interested with [Focusing and Skipping section](https://cljdoc.org/d/lambdaisland/kaocha/1.0.700/doc/6-focusing-and-skipping).

### Implementing Bot
![Bot Sequence Diagram](/assets/overview-xkcd-bot-sequence-diagram.png)

The Bot get latest chat from Telegram. In response, there are chat ids and messages. [Bot will try converting each chat's messages to command](https://github.com/binilinlquad/comic-bot/blob/5e48a9edac7100b82aa03d927ca86ba03169caef/src/com/gandan/bot.clj#L10). [Recognized commands](https://github.com/binilinlquad/comic-bot/blob/5e48a9edac7100b82aa03d927ca86ba03169caef/src/com/gandan/bot.clj#L48) are:
- `/start` which bot reply with welcome message
- `/latest` which bot reply with latest xkcd comic strip

If message is not recognized commands, then Bot will drop and processing the next message.

After finishing processing command, Bot will wait 5 minutes before starting again.
Complete implementation can be found in [Comic-Bot](https://github.com/binilinlquad/comic-bot).

# Retrospective
- REPL is fun. I can test and explore interactively.
- Tutorials are frequently need to be read with others source/repo/blog. Clojure may be intended for experience programmmers(?)

# Several blog and tutorial that I read 
- [ClojureDocs](https://clojuredocs.org/) for providing functions descriptions and samples
- [deps](https://clojure.org/guides/deps_and_cli) as introduction to deps
- [Clojure + deps.edn, a basic guide by tomekw](https://tomekw.com/clojure-deps-edn-a-basic-guide/)
- [Clojureverse](https://clojureverse.org/) where I find lot of interesting things

# Disclaimer
- [xkcd](https://xkcd.com/) is funny and informative comic strip by Randall Munroe. Read it if you weren't.
- Diagram were created with [UMLet](https://www.umlet.com/) and [WebSequenceDiagrams](https://www.websequencediagrams.com/) 
