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

(deftest test-97
  (is (= (pascal 1) [1]))
  (is (= (map pascal (range 1 6))
   [     [1]
        [1 1]
       [1 2 1]
      [1 3 3 1]
     [1 4 6 4 1]]))
  (is (= (pascal 11)
   [1 10 45 120 210 252 210 120 45 10 1])))
       
(run-tests)
</code></pre>
