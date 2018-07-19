---
layout: post
title: 4clojure Problems 100-101
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn lcm [& args]
   (let [gcd (fn [a b] (if (zero? b) a (recur b (mod a b))))]
     (/ (reduce * args) (reduce gcd args))))

(deftest test-100
  (is (== (lcm 2 3) 6))
  (is (== (lcm 5 3 7) 105)))

;; TODO:
;; Figure out how to make it work with ratios in cljs:
;; (== (__ 1/3 2/5) 2)
;; (== (__ 3/4 1/6) 3/2)
;; (== (__ 7 5/7 2 3/5) 210)

(defn lev [s t]
  (let [f (fn [f s t]
            (cond
              (empty? s) (count t)
              (empty? t) (count s)
              :else (let [cost (if (= (first s) (first t)) 0 1)]
                      (min (inc (f f (rest s) t))
                           (inc (f f s (rest t)))
                           (+ cost (f f (rest s) (rest t)))))))
        g (memoize f)]
    (g g s t)))

(deftest test-101
  (is (= (lev "kitten" "sitting") 3))
  (is (= (lev "closure" "clojure") (lev "clojure" "closure") 1))
  (is (= (lev "xyx" "xyyyx") 2))
  (is (= (lev "" "123456") 6))
  (is (= (lev "Clojure" "Clojure") (lev "" "") (lev [] []) 0))
  (is (= (lev [1 2 3 4] [0 2 3 4 5]) 2))
  (is (= (lev '(:a :b :c :d) '(:a :d)) 2))
  (is (= (lev "ttttattttctg" "tcaaccctaccat") 10))
  (is (= (lev "gaattctaatctc" "caaacaaaaaattt") 9)))

(run-tests)
</code></pre>
