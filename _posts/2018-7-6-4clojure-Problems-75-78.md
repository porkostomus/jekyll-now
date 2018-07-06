---
layout: post
title: 4clojure-Problems-75-78
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn totient [a]
  (count
    (for [b (range a)
          :when (not-any? #(= 0 (rem a %) (rem b %)) (range 2 a))]
      b)))

(deftest test-75
  (is (= (totient 1) 1))
  (is (= (totient 10) (count '(1 3 7 9)) 4))
  (is (= (totient 40) 16))
  (is (= (totient 99) 60)))
  
(defn anagram [c]
  (set (for [[_ g] (group-by frequencies c)
            :when (next g)]               
        (set g))))

(deftest test-77
  (is (= (anagram ["meat" "mat" "team" "mate" "eat"]) #{#{"meat" "team" "mate"}}))
  (is (= (anagram ["veer" "lake" "item" "kale" "mite" "ever"]) #{#{"veer" "ever"} #{"lake" "kale"} #{"mite" "item"}})))
  
(defn my-trampoline [f & x]
  (if (fn? f)
    (my-trampoline (apply f x))
    f))

(deftest test-78
  (is (= (letfn [(triple [x] #(sub-two (* 3 x)))
     (sub-two [x] #(stop?(- x 2)))
       (stop? [x] (if (> x 50) x #(triple x)))]
         (my-trampoline triple 2)) 82))
  (is (= (letfn [(my-even? [x] (if (zero? x) true #(my-odd? (dec x))))
  (my-odd? [x] (if (zero? x) false #(my-even? (dec x))))]
    (map (partial my-trampoline my-even?) (range 6)))
    [true false true false true false])))
  
(run-tests)
</code></pre>
