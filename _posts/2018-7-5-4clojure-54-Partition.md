---
layout: post
title: 4clojure-54-Partition
---

Returns a sequence of lists of no less than x items each.

Source for ```partition``` function:

    user=> (source partition)
    (defn partition                                
    "Returns a lazy sequence of lists of n items each, at offsets step
    apart. If step is not supplied, defaults to n, i.e. the partitions
    do not overlap. If a pad collection is supplied, use its elements as
    necessary to complete last partition upto n items. In case there are
    not enough padding elements, return a partition with less than n items."
    {:added "1.0"
     :static true}
    ([n coll]
      (partition n n coll))
    ([n step coll]
     (lazy-seq
       (when-let [s (seq coll)]
         (let [p (doall (take n s))]
           (when (= n (count p))
             (cons p (partition n step (nthrest s step))))))))
    ([n step pad coll]
     (lazy-seq
       (when-let [s (seq coll)]
         (let [p (doall (take n s))]
           (if (= n (count p))
             (cons p (partition n step pad (nthrest s step)))
             (list (take n (concat p pad)))))))))
    nil

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn partition-seq [n s]
  (loop [c s partitioned []] (if (< (count c) n) partitioned (recur (drop n c) (conj partitioned (take n c))))))
  
(deftest partition-test
  (is (= (partition-seq 3 (range 9)) '((0 1 2) (3 4 5) (6 7 8))))
  (is (= (partition-seq 2 (range 8)) '((0 1) (2 3) (4 5) (6 7))))
  (is (= (partition-seq 3 (range 8)) '((0 1 2) (3 4 5)))))

(run-tests)
</code></pre>
