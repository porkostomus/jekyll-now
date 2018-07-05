---
layout: post
title: Live Clojurescript Activated
---

<pre><code class="language-klipse">(defn fib [a b] 
  (lazy-seq (cons a (fib b (+ a b)))))
(take 13 (fib 0 1))
</code></pre>

Change the code and it is re-evaluated.
No more blogging *about* code... *include* it.

We can test the above Fibonacci function:

<pre><code class="language-klipse">(:use '[cljs.test :refer-macros [deftest is testing run-tests]])
(deftest fib-test
  (is (= (take 1 (fib 0 1)) '(0))))
</code></pre>

Here is a simple greeter function:

<pre><code class="language-klipse">(defn greet [name] 
  (str "What up, " name "!"))
(greet "Homie")
</code></pre>

This is possible because of [Klipse](https://github.com/viebel/klipse).
