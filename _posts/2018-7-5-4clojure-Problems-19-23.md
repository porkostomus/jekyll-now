---
layout: post
title: 4clojure-Problems-19-23
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn my-last [s]
  (if (next s)
          (recur (next s))
          (first s)))
  
(deftest test-19
  (is (= (my-last [1 2 3 4 5]) 5))
  (is (= (my-last '(5 4 3)) 3))
  (is (= (my-last ["b" "c" "d"]) "d")))

(defn penultimate [s]
  (second (reverse s)))

(deftest test-20
  (is (= (penultimate (list 1 2 3 4 5)) 4))
  (is (= (penultimate ["a" "b" "c"]) "b"))
  (is (= (penultimate [[1 2] [3 4]]) [1 2])))
  
(defn nth-element [s n]
  (last (take (inc n) s)))

(deftest test-21
  (is (= (nth-element '(4 5 6 7) 2) 6))
  (is (= (nth-element [:a :b :c] 0) :a))
  (is (= (nth-element [1 2 3 4] 1) 2))
  (is (= (nth-element '([1 2] [3 4] [5 6]) 2) [5 6])))
  
(defn count-elements [s]
  (loop [x s acc 0]
    (if (empty? x)
         acc
        (recur (rest x) (inc acc)))))

(deftest test-22
  (is (= (count-elements '(1 2 3 3 1)) 5))
  (is (= (count-elements "Hello World") 11))
  (is (= (count-elements [[1 2] [3 4] [5 6]]) 3))
  (is (= (count-elements '(13)) 1))
  (is (= (count-elements '(:a :b :c)) 3)))
  
(defn reverse-seq [s]
  (reduce conj () s))

(deftest test-23
  (is (= (reverse-seq [1 2 3 4 5]) [5 4 3 2 1]))
  (is (= (reverse-seq (sorted-set 5 7 2 7)) '(7 5 2)))
  (is (= (reverse-seq [[1 2][3 4][5 6]]) [[5 6][3 4][1 2]])))

(run-tests)
</code></pre>
