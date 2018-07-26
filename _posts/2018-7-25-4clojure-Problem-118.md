---
layout: post
title: 4clojure Problem 118
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn mymap [f l]
  (rest (reductions #(f %2) 0 l)))

(deftest test-118
  (is (= [3 4 5 6 7]
   (mymap inc [2 3 4 5 6])))
  (is (= (repeat 10 nil)
   (mymap (fn [_] nil) (range 10))))
  (is (= [1000000 1000001]
   (->> (mymap inc (range))
        (drop (dec 1000000))
        (take 2)))
(= [1000000 1000001]
   (->> (mymap inc (range))
        (drop (dec 1000000))
        (take 2)))))

(run-tests)
</code></pre>
