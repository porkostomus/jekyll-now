---
layout: post
title: 4clojure Problems 88-89
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn sym-diff [a b]
  (into (set (remove b a)) (remove a b)))

(run-tests)
</code></pre>
