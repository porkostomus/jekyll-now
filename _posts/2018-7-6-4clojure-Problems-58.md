---
layout: post
title: 4clojure-Problems-58
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn mycomp [f & gs]
  (if gs
    #(f (apply (apply mycomp gs) (conj %& %)))
    f))

(deftest test-58
  (is (= [3 2 1] ((mycomp rest reverse) [1 2 3 4])))
  (is (= 5 ((mycomp (partial + 3) second) [1 2 3 4])))
  (is (= true ((mycomp zero? #(mod % 8) +) 3 5 7 9)))
  (is (= "HELLO" ((mycomp #(.toUpperCase %) #(apply str %) take) 5 "hello world"))))
 
(defn myjuxt [& f]
  (fn [& a]
    (map #(apply % a) f)))
  
(deftest test-59
  (is (= [21 6 1] ((myjuxt + max min) 2 3 5 1 6 4)))
  (is (= ["HELLO" 5] ((myjuxt #(.toUpperCase %) count) "hello")))
  (is (= [2 6 4] ((myjuxt :a :c :b) {:a 2, :b 4, :c 6, :d 8 :e 10})))) 
 
(run-tests)
</code></pre>
