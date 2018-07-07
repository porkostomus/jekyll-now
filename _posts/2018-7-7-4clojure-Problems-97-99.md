---
layout: post
title: 4clojure Problems 97-99
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn pascal [n]
  (loop [x 1 l [1]]
    (if (= x n) l
      (recur (inc x)(vec (map + (cons 0 l)(conj l 0)))))))

(deftest test-97
  (is (= (pascal 1) [1]))
  (is (= (map pascal (range 1 6))
   [     [1]
        [1 1]
       [1 2 1]
      [1 3 3 1]
     [1 4 6 4 1]]))
  (is (= (pascal 11)
   [1 10 45 120 210 252 210 120 45 10 1])))

(defn classes [f c]
  (set (map set (vals (group-by f c)))))

(deftest test-98
  (is (= (classes #(* % %) #{-2 -1 0 1 2})
   #{#{0} #{1 -1} #{2 -2}}))
  (is (= (classes #(rem % 3) #{0 1 2 3 4 5 })
   #{#{0 3} #{1 4} #{2 5}}))
  (is (= (classes identity #{0 1 2 3 4})
   #{#{0} #{1} #{2} #{3} #{4}}))
  (is (= (classes (constantly true) #{0 1 2 3 4})
   #{#{0 1 2 3 4}})))

(defn digits [x y]
  (map #(- (int %) (int \0)) (str (* x y))))

(deftest test-99
  (is (= (digits 1 1) [1]))
  (is (= (digits 99 9) [8 9 1]))
  (is (= (digits 999 99) [9 8 9 0 1])))
       
(run-tests)
</code></pre>
