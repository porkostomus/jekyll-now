---
layout: post
title: 4clojure-Problems-66
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn gcd [a b]
  (if (= 0 b) a (recur b (mod a b))))

(deftest test-66
  (is (= (gcd 2 4) 2))
  (is (= (gcd 10 5) 5))
  (is (= (gcd 5 7) 1))
  (is (= (gcd 1023 858) 33)))
  
(defn primes [n] 
  (->>
  (range)
  (drop 2)
  (filter (fn [x] (every? #(< 0 (mod x %)) (range 2 x))))
  (take n)))

(deftest test-67
  (is (= (primes 2) [2 3]))
  (is (= (primes 5) [2 3 5 7 11]))
  (is (= (last (primes 100)) 541)))
  
(defn my-merge-with [f & ms]
  (reduce (fn [am m]
            (into am (for [[k v] m]
                       (if (contains? am k)
                         [k (f (am k) v)]
                         [k v]))))
          ms))

(deftest test-69
  (is (= (my-merge-with * {:a 2, :b 3, :c 4} {:a 2} {:b 2} {:c 5}) {:a 4, :b 6, :c 20}))
  (is (= (my-merge-with - {1 10, 2 20} {1 3, 2 10, 3 15}) {1 7, 2 10, 3 15}))
  (is (= (my-merge-with concat {:a [3], :b [6]} {:a [4 5], :c [8 9]} {:b [7]}) {:a [3 4 5], :b [6 7], :c [8 9]})))
  
(run-tests)
</code></pre>
