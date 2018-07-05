---
layout: post
title: Live Clojurescript Snippets!
---

<pre><code class="language-klipse">(def fib-seq-seq
  ((fn fib [a b] 
     (lazy-seq (cons a (fib b (+ a b)))))
   0 1))
(take 13 fib-seq-seq)
</code></pre>

<pre><code class="language-klipse">(map inc [1 2 3])
</code></pre>
