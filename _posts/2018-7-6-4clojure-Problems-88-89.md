---
layout: post
title: 4clojure Problems 88-89
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn sym-diff [a b]
  (into (set (remove b a)) (remove a b)))

(deftest test-88
  (is (= (sym-diff #{1 2 3 4 5 6} #{1 3 5 7}) #{2 4 6 7}))
  (is (= (sym-diff #{:a :b :c} #{}) #{:a :b :c}))
  (is (= (sym-diff #{} #{4 5 6}) #{4 5 6}))
  (is (= (sym-diff #{[1 2] [2 3]} #{[2 3] [3 4]}) #{[1 2] [3 4]})))

(defn eulerian [e]
  (if (#{0 2} (count (filter odd? (vals (frequencies (mapcat seq e))))))
    (not (next (reduce
                (fn [g e]
                  (let [[a b] (map (fn [n] (or (some #(if (% n) %) g) #{n})) e)]
                    (conj (disj g a b) (into a b))))
                #{}
                e)))
    false))

(deftest test-89
  (is (= true (eulerian [[:a :b]])))
  (is (= false (eulerian [[:a :a] [:b :b]])))
  (is (= false (eulerian [[:a :b] [:a :b] [:a :c] [:c :a]
               [:a :d] [:b :d] [:c :d]])))
  (is (= true (eulerian [[1 2] [2 3] [3 4] [4 1]])))
  (is (= true (eulerian [[:a :b] [:a :c] [:c :b] [:a :e]
              [:b :e] [:a :d] [:b :d] [:c :e]
              [:d :e] [:c :f] [:d :f]])))
  (is (= false (eulerian [[1 2] [2 3] [2 4] [2 5]]))))

(defn cartesian [x y]
  (set (for [a x b y] [a b])))

(deftest test-90
  (is (= (cartesian #{"ace" "king" "queen"} #{"♠" "♥" "♦" "♣"})
   #{["ace"   "♠"] ["ace"   "♥"] ["ace"   "♦"] ["ace"   "♣"]
     ["king"  "♠"] ["king"  "♥"] ["king"  "♦"] ["king"  "♣"]
     ["queen" "♠"] ["queen" "♥"] ["queen" "♦"] ["queen" "♣"]}))
  (is (= (cartesian #{1 2 3} #{4 5})
   #{[1 4] [2 4] [3 4] [1 5] [2 5] [3 5]}))
  (is (= 300 (count (cartesian (into #{} (range 10))
                  (into #{} (range 30)))))))

(run-tests)
</code></pre>
