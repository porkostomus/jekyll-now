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

(run-tests)
</code></pre>
