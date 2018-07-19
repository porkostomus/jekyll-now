---
layout: post
title: 4clojure Problems 104-105
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn f [[n & a] [s & b] o i]
  (if n
    (f a b (into o (repeat (int (/ i n)) s)) (rem i n))
    (apply str o)))
[1000 900 500 400 100 90 50 40 10  9 5  4 1]
'[  M  CM   D  CD   C XC  L XL  X IX V IV I]
[]


(run-tests)
</code></pre>
