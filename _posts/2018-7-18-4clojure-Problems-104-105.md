---
layout: post
title: 4clojure Problems 104-105
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn roman [x]
  (cond
    (<= 1000 x) (str "M" (roman (- x 1000)))
    (<= 900 x) (str "CM" (roman (- x 900)))
    (<= 500 x) (str "D" (roman (- x 500)))
    (<= 400 x) (str "CD" (roman (- x 400)))
    (<= 100 x) (str "C" (roman (- x 100)))
    (<= 90 x) (str "XC" (roman (- x 90)))
    (<= 50 x) (str "L" (roman (- x 50)))
    (<= 40 x) (str "XL" (roman (- x 40)))
    (<= 10 x) (str "X" (roman (- x 10)))
    (<= 9 x) (str "IX" (roman (- x 9)))
    (<= 5 x) (str "V" (roman (- x 5)))
    (<= 4 x) (str "IV" (roman (- x 4)))
    (<= 1 x) (str "I" (roman (- x 1)))
    true ""))

(deftest test-104
  (is (= "I" (roman 1)))
  (is (= "I" (roman 1)))
  (is (= "XXX" (roman 30)))
  (is (= "IV" (roman 4)))
  (is (= "CXL" (roman 140)))
  (is (= "DCCCXXVII" (roman 827)))
  (is (= "MMMCMXCIX" (roman 3999)))
  (is (= "XLVIII" (roman 48))))

(defn key-val [c]
  (loop [[f & r] c, kvm {}]
    (if (nil? f)
      kvm
     (let [[vs l] (split-with (complement keyword?) r)]
       (recur l (assoc kvm f vs))))))

(deftest test-105
  (is (= {} (key-val [])))
  (is (= {:a [1]} (key-val [:a 1])))
  (is (= {:a [1], :b [2]} (key-val [:a 1, :b 2])))
  (is (= {:a [1 2 3], :b [], :c [4]} (key-val [:a 1 2 3 :b :c 4]))))
(run-tests)
</code></pre>
