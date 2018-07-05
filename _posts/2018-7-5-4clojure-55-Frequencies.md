---
layout: post
title: 4clojure-54-Frequencies
---

Returns a map containing the number of occurences of each distinct item in a sequence.

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn freqs [s]
  (loop [s s freq-map {}]
    (if (empty? s)
      freq-map
      (recur (rest s)
        (assoc freq-map (first s) (inc (get freq-map (first s) 0)))))))
  
(deftest partition-test
  (is (= (freqs [1 1 2 3 2 1 1]) {1 4, 2 2, 3 1}))
  (is (= (freqs [:b :a :b :a :b]) {:a 2, :b 3}))
  (is (= (freqs '([1 2] [1 3] [1 3])) {[1 2] 1, [1 3] 2})))

(run-tests)
</code></pre>
