---
layout: post
title: 4clojure-56-Distinct
---

Removes duplicates from a sequence. Order of the items must be maintained.

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn deduper [coll]
  (loop [seen #{} s (seq coll) res []]
    (if (empty? s)
      res
      (let [f (first s)]
        (recur
          (conj seen f)
          (rest s)
          (if (contains? seen f)
            res
            (conj res f)))))))
  
(deftest partition-test
  (is (= (deduper [1 2 1 3 1 2 4]) [1 2 3 4]))
  (is (= (deduper [:a :a :b :b :c :c]) [:a :b :c]))
  (is (= (deduper '([2 4] [1 2] [1 3] [1 3])) '([2 4] [1 2] [1 3]))
  (is (= (deduper (range 50)) (range 50)))))

(run-tests)
</code></pre>
