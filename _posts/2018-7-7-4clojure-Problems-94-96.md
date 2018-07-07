---
layout: post
title: 4clojure Problems 94-96
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn conway [board]
  (let [r (range (count board))
       v [-1 0 1]
       a \#]
   (for [y r]
     (apply str (for [x r c [(count
                              (for [j v
                                    k v
                                    :when (= a (get-in board [(+ y j) (+ x k)]))]
                                1))]]
                  (if (or (= c 3) (and (= c 4) (= a (get-in board [y x]))))
                    a
                    \ ))))))

(deftest test-94
  (is (= (conway ["      "  
        " ##   "
        " ##   "
        "   ## "
        "   ## "
        "      "])
   ["      "  
    " ##   "
    " #    "
    "    # "
    "   ## "
    "      "]))
(is (= (conway ["     "
        "     "
        " ### "
        "     "
        "     "]))
   ["     "
    "  #  "
    "  #  "
    "  #  "
    "     "])
(is (= (conway ["      "
        "      "
        "  ### "
        " ###  "
        "      "
        "      "])
   ["      "
    "   #  "
    " #  # "
    " #  # "
    "  #   "
    "      "])))
  
(defn tree? [n]
  (or (nil? n)
      (and (coll? n)
           (= 3 (count n))
           (every? tree? (rest n)))))

(deftest test-95
  (is (= (tree? '(:a (:b nil nil) nil))
   true))
  (is (= (tree? '(:a (:b nil nil)))
   false))
  (is (= (tree? [1 nil [2 [3 nil nil] [4 nil nil]]])
   true))
  (is (= (tree? [1 [2 nil nil] [3 nil nil] [4 nil nil]])
   false))
  (is (= (tree? [1 [2 [3 [4 nil nil] nil] nil] nil])
   true))
  (is (= (tree? [1 [2 [3 [4 false nil] nil] nil] nil])
   false))
  (is (= (tree? '(:a nil ()))
   false))
  (is (= (tree? '(:a nil ()))
   false))) 
  
(defn symmetric? [t]
  (= t ((fn m [[v l r]] (if v [v (m r) (m l)])) t)))

(deftest test-96
  (is (= (symmetric? '(:a (:b nil nil) (:b nil nil))) true))
  (is (= (symmetric? '(:a (:b nil nil) nil)) false))
  (is (= (symmetric? '(:a (:b nil nil) (:c nil nil))) false))
  (is (= (symmetric? [1 [2 nil [3 [4 [5 nil nil] [6 nil nil]] nil]]
          [2 [3 nil [4 [6 nil nil] [5 nil nil]]] nil]])
   true))
    (is (= (symmetric? [1 [2 nil [3 [4 [5 nil nil] [6 nil nil]] nil]]
          [2 [3 nil [4 [5 nil nil] [6 nil nil]]] nil]])
   false))
      (is (= (symmetric? [1 [2 nil [3 [4 [5 nil nil] [6 nil nil]] nil]]
          [2 [3 nil [4 [6 nil nil] nil]] nil]])
   false)))

(run-tests)
</code></pre>
