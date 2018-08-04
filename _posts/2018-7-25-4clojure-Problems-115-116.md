---
layout: post
title: 4clojure 115-116
---

## 115 The Balance of N

A balanced number is one whose component digits have the same sum on the left and right halves of the number. Write a function which accepts an integer n, and returns true iff n is balanced.

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))
  
(defn bal-num [n]
  (let [s (map #(- (int %) 48) (str n))
        l (/ (count s) 2)
        [a b] (map #(apply + (take l %)) [s (into () s)])]
    (= a b)))

(deftest test-115
  (is (= true (bal-num 11)))
  (is (= true (bal-num 121)))
  (is (= false (bal-num 123)))
  (is (= true (bal-num 0)))
  (is (= false (bal-num 88099)))
  (is (= true (bal-num 89098)))
  (is (= true (bal-num 89089)))
  (is (= (take 20 (filter bal-num (range)))
   [0 1 2 3 4 5 6 7 8 9 11 22 33 44 55 66 77 88 99 101])))

; 116 Prime Sandwich

; A balanced prime is a prime number which is also the mean of the primes directly before and after it in the sequence of valid primes. Create a function which takes an integer n, and returns true iff it is a balanced prime.

(defn ps [n]
  (first (for [o (range 1 (- n 2))
              [a b c] [(for [x [(- n o) (+ n o) n]]
                         (every? (fn [b] (> (rem x b) 0)) (range 2 x)))]
              :when (or a b)]
           (and a b c))))

(deftest test-116
  (is (= false (ps 4)))
  (is (= true (ps 563)))
  (is (= 1103 (nth (filter ps (range)) 15))))

(run-tests)
</code></pre>
