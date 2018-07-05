---
layout: post
title: 4clojure-54-Frequencies
---

Returns a map containing the number of occurences of each distinct item in a sequence.

Here is the source for the ```frequencies``` function:

    user=> (source frequencies)
    (defn frequencies
    "Returns a map from distinct items in coll to the number of times
    they appear."
    {:added "1.2"
     :static true}
    [coll]
    (persistent!
     (reduce (fn [counts x]
             (assoc! counts x (inc (get counts x 0))))
           (transient {}) coll)))
    nil

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn freqs [s]
  (apply merge-with + (for [i s] {i 1})))
  
(deftest partition-test
  (is (= (freqs [1 1 2 3 2 1 1]) {1 4, 2 2, 3 1}))
  (is (= (freqs [:b :a :b :a :b]) {:a 2, :b 3}))
  (is (= (freqs '([1 2] [1 3] [1 3])) {[1 2] 1, [1 3] 2})))

(run-tests)
</code></pre>
