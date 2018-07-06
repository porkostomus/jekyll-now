---
layout: post
title: 4clojure-Problems-84-85
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn trans-clojure [r]
  (loop [s r]
    (let [n (into s
                 (for [[a b] s [c d] s 
                       :when (= b c)] 
                   [a d]))]
      (if (= n s) n (recur n))))

  
(run-tests)
</code></pre>
