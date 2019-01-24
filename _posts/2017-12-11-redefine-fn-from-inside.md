---
layout: post
title: (TIL) Clojure permit redefine function from itself
---
For example, please see this code below
~~~ clojure
(defn hallo
    (defn hallo "Hello"))
nil

(hallo)
nil

(hallo)
"Hello"
~~~
At first, I define hallo ass function which is will redefine hallo as function returning string "Hello"

I invoke hallo and it will redefine itself

Invoke again and hallo returning string "Hello"
