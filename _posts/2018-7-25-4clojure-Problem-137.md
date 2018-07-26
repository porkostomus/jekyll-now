---
layout: post
title: 4clojure Problem 137
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn digits [n b]
  (if (< n b)
    [n]
    (conj (digits (quot n b) b) (rem n b))))

(deftest test-137
  (is (= [1 2 3 4 5 0 1] (digits 1234501 10)))
  (is (= [0] (digits 0 11)))
  (is (= [1 0 0 1] (digits 9 2)))
  (is (= [1 0] (let [n (rand-int 100000)](digits n n)))))

; (is (= [16 18 5 24 15 1] (digits Integer/MAX_VALUE 42)))

(run-tests)
</code></pre>
