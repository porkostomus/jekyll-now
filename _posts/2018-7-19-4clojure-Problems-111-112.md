---
layout: post
title: 4clojure Problems 111-112
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))
  
(defn cw [word board]
  (let [across (map #(clojure.string/escape % {\space "", \_ \.}) board)
        down (apply map str across)]   ;; transpose the board so down becomes across
    (string? (->> (concat across down)
                  (mapcat #(clojure.string/split % #"#"))
                  (some #(re-matches (re-pattern %) word))))))

(deftest test-111
  (is (= true  (cw "the" ["_ # _ _ e"])))
  (is (= false (cw "the" ["c _ _ _"
                    "d _ # e"
                    "r y _ _"])))
  (is (= true  (cw "joy" ["c _ _ _"
                    "d _ # e"
                    "r y _ _"])))
  (is (= false (cw "joy" ["c o n j"
                    "_ _ y _"
                    "r _ _ #"])))
  (is (= true  (cw "clojure" ["_ _ _ # j o y"
                        "_ _ o _ _ _ _"
                        "_ _ f _ # _ _"]))))
 
(defn sh [n [x & r]]
  (if x
    (if (sequential? x)
      (let [sub (sh n x)]
        (cons sub (sh (- n (reduce + (flatten sub))) r)))
      (if (<= x n)
        (cons x (sh (- n x) r))
        ()))))

(deftest test-112
  (is (=  (sh 10 [1 2 [3 [4 5] 6] 7])
   '(1 2 (3 (4)))))
  (is (=  (sh 30 [1 2 [3 [4 [5 [6 [7 8]] 9]] 10] 11])
   '(1 2 (3 (4 (5 (6 (7))))))))
  (is (=  (sh 9 (range))
   '(0 1 2 3)))
  (is (=  (sh 1 [[[[[1]]]]])
   '(((((1)))))))
  (is (=  (sh 0 [1 2 [3 [4 5] 6] 7])
   '()))
  (is (=  (sh 0 [0 0 [0 [0]]])
   '(0 0 (0 (0)))))
  (is (=  (sh 1 [-10 [1 [2 3 [4 5 [6 7 [8]]]]]])
   '(-10 (1 (2 3 (4)))))))

(run-tests)
</code></pre>
