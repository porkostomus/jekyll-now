---
layout: post
title: 4clojure Problems 115-116
---

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
