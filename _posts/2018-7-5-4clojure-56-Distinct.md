---
layout: post
title: 4clojure-56-Distinct
---

Remove duplicates from a sequence. Order of the items must be maintained.

May not use the ```distinct``` function:

    user=> (source distinct)
    (defn distinct
    "Returns a lazy sequence of the elements of coll with duplicates removed.
    Returns a stateful transducer when no collection is provided."
    {:added "1.0"
     :static true}
    ([]
    (fn [rf]
     (let [seen (volatile! #{})]
       (fn
         ([] (rf))
         ([result] (rf result))
         ([result input]
          (if (contains? @seen input)
            result
            (do (vswap! seen conj input)
                (rf result input))))))))
    ([coll]
    (let [step (fn step [xs seen]
                (lazy-seq
                  ((fn [[f :as xs] seen]
                     (when-let [s (seq xs)]
                       (if (contains? seen f)
                         (recur (rest s) seen)
                         (cons f (step (rest s) (conj seen f))))))
                   xs seen)))]
     (step coll #{}))))
    nil


This exercise continues the theme of taking a built-in function and asking us to re-implement it another way: 

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn deduper [s]
    (reduce #(if ((set %) %2) % (conj % %2)) [] s))
  
(deftest partition-test
  (is (= (deduper [1 2 1 3 1 2 4]) [1 2 3 4]))
  (is (= (deduper [:a :a :b :b :c :c]) [:a :b :c]))
  (is (= (deduper '([2 4] [1 2] [1 3] [1 3])) '([2 4] [1 2] [1 3]))
  (is (= (deduper (range 50)) (range 50)))))

(run-tests)
</code></pre>
