---
layout: post
title: More Live Clojurescript
---

### 4clojure #53: Longest Increasing Subsequence

<pre><code class="language-klipse">(ns live.test
(:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn longest-subseq [s]
  (or (first (filter #(apply < %)
    (mapcat #(partition % 1 s)
      (range (count s) 1 -1))))))
  
(deftest test-numbers
  (is (= (longest-subseq [1 0 1 2 3 0 4 5]) [0 1 2 3]))
  (is (= (longest-subseq [5 6 1 3 2 7]) [5 6]))
  (is (= (longest-subseq [2 3 3 4 5]) [3 4 5]))
  (is (= (longest-subseq [7 6 5 4]) nil)))

(run-tests)
</code></pre>
