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

(run-tests)
</code></pre>
