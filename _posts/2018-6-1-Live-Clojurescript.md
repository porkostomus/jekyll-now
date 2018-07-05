---
layout: post
title: Live Clojurescript!
---

<pre><code class="language-klipse">(def fib-seq
  ((fn fib [a b] 
     (lazy-seq (cons a (fib b (+ a b)))))
   0 1))
(take 13 fib-seq)
</code></pre>
