---
layout: post
title: 4clojure-Problems-58-63
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
 
 (defn my-reductions
  ([f v s]
    (lazy-seq
      (cons v (if (seq s)
                (r f (f v (first s)) (rest s))))))
  ([f s] (r f (first s) (rest s))))

(deftest test-60
  (is (= (take 5 (my-reductions + (range))) [0 1 3 6 10]))
  (is (= (my-reductions conj [1] [2 3 4]) [[1] [1 2] [1 2 3] [1 2 3 4]]))
  (is (= (last (my-reductions * 2 [3 4 5])) (reduce * 2 [3 4 5]) 120)))
 
(defn make-map [keys vals]
  (apply hash-map (interleave keys vals)))

(deftest test-61
  (is (= (make-map [:a :b :c] [1 2 3]) {:a 1, :b 2, :c 3}))
  (is (= (make-map [1 2 3 4] ["one" "two" "three"]) {1 "one", 2 "two", 3 "three"}))
  (is (= (make-map [:foo :bar] ["foo" "bar" "baz"]) {:foo "foo", :bar "bar"})))
 
(defn spaz-out [f init]
       (cons init
         (lazy-seq
           (spaz-out f (f init)))))

(deftest test-62
  (is (= (take 5 (spaz-out #(* 2 %) 1)) [1 2 4 8 16]))
  (is (= (take 100 (spaz-out inc 0)) (take 100 (range))))
  (is (= (take 9 (spaz-out #(inc (mod % 3)) 1)) (take 9 (cycle [1 2 3])))))
  
(defn my-group-by [f s]
  (reduce
(fn [m x] (assoc m (f x) (conj (m (f x) []) x))) 
{} s))

(deftest test-63
  (is (= (my-group-by #(> % 5) #{1 3 6 8}) {false [1 3], true [6 8]}))
  (is (= (my-group-by #(apply / %) [[1 2] [2 4] [4 6] [3 6]]) {1/2 [[1 2] [2 4] [3 6]], 2/3 [[4 6]]}))
  (is (= (my-group-by count [[1] [1 2] [3] [1 2 3] [2 3]]) {1 [[1] [3]], 2 [[1 2] [2 3]], 3 [[1 2 3]]})))
 
(run-tests)
</code></pre>
