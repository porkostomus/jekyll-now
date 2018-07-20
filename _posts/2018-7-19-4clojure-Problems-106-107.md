---
layout: post
title: 4clojure Problems 106-107
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))
  
(defn find-path [s e]
  (loop [opts [s] depth 1]
    (if (some #{e} opts)
      depth
      (letfn [(solutions [n]
                (concat 
                  [(* n 2) (+ n 2)]
                  (if (even? n) [(/ n 2)] [])))]
        (recur (mapcat solutions opts) (inc depth))))))

(deftest test-106
  (is (= 1 (find-path 1 1)))
  (is (= 3 (find-path 3 12)))
  (is (= 3 (find-path 12 3)))
  (is (= 3 (find-path 5 9)))
  (is (= 9 (find-path 9 2)))
  (is (= 5 (find-path 9 12))))

(defn closure [n] #(apply * (repeat n %)))

(deftest test-107
  (is (= 256 ((closure 2) 16), ((closure 8) 2)))
  (is (= [1 8 27 64] (map (closure 3) [1 2 3 4])))
  (is (= [1 2 4 8 16] (map #((closure %) 2) [0 1 2 3 4]))))  
  
(run-tests)
</code></pre>
