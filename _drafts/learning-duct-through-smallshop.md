## Why
- I like learning clojure and want to implement with it
- I hear about [duct](https://github.com/duct-framework/duct) and it seems good start to organize my project
- Compile my newbie experience's. 

## Create new duct project
I use [Leinengen](https://leiningen.org/) to setup my project. I give name "smallshop" with goal to create simple online shop.
1. lein new duct <project name>. Complete options look https://github.com/duct-framework/duct.
   It will produce basic skeleton for it. I add parameters:
   a. +ataraxy : not sure what is right now, but it says router so I think will need it
   b. +postgres : interfacing with database in production
   c. +site : smallshop is web so of course need it
   d. +sqlite : I am thinking to use it in development
   It becomes `lein new duct smallshop +ataraxy +postgres +site +sqlite`
2. Make sure postgres installed and started before start the server.
If not, then you may see error which saying `cannot connect to Http` etc error (will update with error later).
3. Read the documentation for [duct configuration](https://github.com/duct-framework/duct/wiki/Configuration). Beware that module key is different from profile key. Read too about composite key. You will find all of it in config.edn file under project resource's path.

## How to run the application
I am using [Spacemacs](https://www.spacemacs.org/) with installed [Cider](https://develop.spacemacs.org/layers/+lang/clojure/README.html).

Run as specified by duct [Readme](https://github.com/duct-framework/duct/wiki/Getting-Started).

## Replace database connection from postgres with sqlite in development
Setup and running postgresql may not you want to do at early development phase. You can swap postgresql with sqlite.
  dev/resource/dev.edn
  ```
  ;{:connection-uri "jdbc:postgresql://localhost/postgres"} ; use this for postgres
  {:connection-uri "jdbc:sqlite:db/dev.sqlite"}}
  ```

## Replace ataraxy with re-itit
While getting help setup duct for ataraxy in slack clojurians, I heard about re-itit. I find it is good practice to try replace ataraxy with another library.


## Features
- Inventory management

