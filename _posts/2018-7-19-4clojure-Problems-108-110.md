---
layout: post
title: 4clojure Problems 108-110
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))
  
(defn lazy [& s]
  (loop [v (vec s)]
    (let [first-vals (map first v)
          smallest (apply min first-vals)]
      (if (= smallest (apply max first-vals))
        smallest
        (let [i (apply min-key #(nth first-vals %) (range (count v)))]
          (recur (update-in v [i] next)))))))

(deftest test-108
  (is (= 3 (lazy [3 4 5])))
  (is (= 4 (lazy [1 2 3 4 5 6 7] [0.5 3/2 4 19])))
  (is (= 64 (lazy (map #(* % % %) (range))
          (filter #(zero? (bit-and % (dec %))) (range))
          (iterate inc 20)))))

;;TODO: (is (= 7 (lazy (range) (range 0 100 7/6) [2 3 5 7 11 13])))

(defn seq-prons [s]
  (next (iterate #(mapcat (juxt count first)
                    (partition-by identity %)) s)))

(deftest test-110
  (is (= [[1 1] [2 1] [1 2 1 1]] (take 3 (seq-prons [1]))))
  (is (= [3 1 2 4] (first (seq-prons [1 1 1 4 4]))))
  (is (= [1 1 1 3 2 1 3 2 1 1] (nth (seq-prons [1]) 6)))
  (is (= 338 (count (nth (seq-prons [3 2]) 15)))))

(run-tests)
</code></pre>
