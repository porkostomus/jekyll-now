---
layout: post
title: 4clojure Problems 97-98
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn pascal [n]
  (loop [x 1 l [1]]
   (if (= x n) l
       (recur (inc x)(vec (map + (cons 0 l)(conj l 0)))))))
       
(run-tests)
</code></pre>
