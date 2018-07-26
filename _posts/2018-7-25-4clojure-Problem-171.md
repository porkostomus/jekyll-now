---
layout: post
title: 4clojure Problem 171
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn intervals [coll]
  (reverse (reduce (fn [[[a b] & r :as is] n]
                     (if (and a (= (inc b) n))
                       (cons [a n] r)
                       (cons [n n] is)))
                   ()
                   (distinct (sort coll)))))

(deftest test-171
  (is (= (intervals [1 2 3]) [[1 3]]))
  (is (= (intervals [10 9 8 1 2 3]) [[1 3] [8 10]]))
  (is (= (intervals [1 1 1 1 1 1 1]) [[1 1]]))
  (is (= (intervals []) []))
  (is (= (intervals [19 4 17 1 3 10 2 13 13 2 16 4 2 15 13 9 6 14 2 11])
       [[1 4] [6 6] [9 11] [13 17] [19 19]])))

(run-tests)
</code></pre>
