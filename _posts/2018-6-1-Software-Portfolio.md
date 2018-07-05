---
layout: post
title: Software Portfolio
---

Ap<p>And now, we are going to <strong>klipsify</strong> this code snippet:</p>


<pre><code class="language-klipse">(def fib-seq-seq
  ((fn fib [a b] 
     (lazy-seq (cons a (fib b (+ a b)))))
   0 1))
(take 13 fib-seq-seq)
</code></pre>
