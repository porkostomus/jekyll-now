---
layout: post
title: 4clojure-Problems-66
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn gcd [a b]
  (if (= 0 b) a (recur b (mod a b))))

(deftest test-66
  (is (= (gcd 2 4) 2))
  (is (= (gcd 10 5) 5))
  (is (= (gcd 5 7) 1))
  (is (= (gcd 1023 858) 33)))
  
(run-tests)
</code></pre>
