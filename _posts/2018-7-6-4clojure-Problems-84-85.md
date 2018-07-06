---
layout: post
title: 4clojure-Problems-84-85
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is testing run-tests]]))
  
(defn trans-closure [r]
  (loop [s r]
    (let [n (into s
                  (for [[a b] s [c d] s 
                        :when (= b c)] 
                    [a d]))]
      (if (= n s) n (recur n)))))

(deftest test-84
  (is (let [divides #{[8 4] [9 3] [4 2] [27 9]}]
    (= (trans-closure divides) #{[4 2] [8 4] [8 2] [9 3] [27 9] [27 3]})))
  (is (let [more-legs
      #{["cat" "man"] ["man" "snake"] ["spider" "cat"]}]
  (= (trans-closure more-legs)
     #{["cat" "man"] ["cat" "snake"] ["man" "snake"]
       ["spider" "cat"] ["spider" "man"] ["spider" "snake"]})))
  (is (let [progeny
      #{["father" "son"] ["uncle" "cousin"] ["son" "grandson"]}]
  (= (trans-closure progeny)
     #{["father" "son"] ["father" "grandson"]
       ["uncle" "cousin"] ["son" "grandson"]}))))

  
(run-tests)
</code></pre>
