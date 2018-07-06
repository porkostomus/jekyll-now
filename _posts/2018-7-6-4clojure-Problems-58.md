---
layout: post
title: 4clojure-Problems-39-56
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn mycomp [f & gs]
  (if gs
    #(f (apply (apply cmp gs) (conj %& %)))
    f))

(deftest test-58
  (is (= [3 2 1] ((mycomp rest reverse) [1 2 3 4]))))
 
(run-tests)
</code></pre>
