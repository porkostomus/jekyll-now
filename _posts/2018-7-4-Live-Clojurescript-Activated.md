---
layout: post
title: Live Clojurescript Activated
---

<pre><code class="language-klipse">(defn fib [a b] 
  (lazy-seq (cons a (fib b (+ a b)))))
(take 13 (fib 0 1))
</code></pre>



<pre><code class="language-klipse">(defn greet [name] 
  (str "What up, " name "!"))
(greet "Homie")
</code></pre>
