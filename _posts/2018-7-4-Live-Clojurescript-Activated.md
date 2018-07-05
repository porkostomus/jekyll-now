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

<pre><code class="language-klipse">(ns my-project.tests
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))

(defn fib [a b] 
  (lazy-seq (cons a (fib b (+ a b)))))

(deftest test-numbers
  (is (= (take 1 (fib 0 1)) '(0)))
  (is (= (take 2 (fib 0 1)) '(0 1)))
  (is (= (take 3 (fib 0 1)) '(0 1 1)))
  (is (= (take 4 (fib 0 1)) '(0 1 1 2)))
  (is (= (take 5 (fib 0 1)) '(0 1 1 2 3)))
  (is (= (take 6 (fib 0 1)) '(0 1 1 2 3 5)))
  (is (= (take 7 (fib 0 1)) '(0 1 1 2 3 5 8)))
  (is (= (take 8 (fib 0 1)) '(0 1 1 2 3 5 8 13)))
  (is (= (take 9 (fib 0 1)) '(0 1 1 2 3 5 8 13 21)))
  (is (= (take 10 (fib 0 1)) '(0 1 1 2 3 5 8 13 21 34))))
  
(run-tests)
</code></pre>

Here is a simple greeter function:

<pre><code class="language-klipse">(defn greet [name] 
  (str "What up, " name "!"))
(greet "Homie")
</code></pre>

This is possible because of [Klipse](https://github.com/viebel/klipse).
