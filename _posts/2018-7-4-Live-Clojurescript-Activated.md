---
layout: post
title: Live Clojurescript Activated
---

<pre><code class="language-klipse">(defn fib [a b] 
  (lazy-seq (cons a (fib b (+ a b)))))
(take 13 (fib 0 1))
</code></pre>

You can change the code however you want.

Here is a simple greeter function:

<pre><code class="language-klipse">(defn greet [name] 
  (str "What up, " name "!"))
(greet "Homie")
</code></pre>

This is possible because of [Klipse](https://github.com/viebel/klipse).
